local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Evita criar duas cópias da interface.
local oldGui = playerGui:FindFirstChild("KatakuriOpenSource")
if oldGui then
    oldGui:Destroy()
end

local CONFIG = {
    Title = "KATAKURI",
    Subtitle = "OPEN SOURCE",
    Accent = Color3.fromRGB(145, 75, 255),
    Background = Color3.fromRGB(20, 20, 27),
    Panel = Color3.fromRGB(29, 29, 39),
    Text = Color3.fromRGB(245, 245, 250),
    Muted = Color3.fromRGB(155, 155, 170),
}

local gui = Instance.new("ScreenGui")
gui.Name = "KatakuriOpenSource"
gui.ResetOnSpawn = false
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
gui.Parent = playerGui

local function create(className, properties, parent)
    local object = Instance.new(className)
    for property, value in pairs(properties) do
        object[property] = value
    end
    object.Parent = parent
    return object
end

local function corner(parent, radius)
    create("UICorner", {CornerRadius = UDim.new(0, radius or 8)}, parent)
end

local function notify(message)
    local toast = create("TextLabel", {
        Name = "Notification",
        AnchorPoint = Vector2.new(1, 1),
        Position = UDim2.new(1, -18, 1, -18),
        Size = UDim2.fromOffset(260, 42),
        BackgroundColor3 = CONFIG.Panel,
        TextColor3 = CONFIG.Text,
        Text = tostring(message),
        TextSize = 14,
        Font = Enum.Font.GothamMedium,
        TextWrapped = true,
        ZIndex = 20,
    }, gui)
    corner(toast, 9)
    create("UIStroke", {Color = CONFIG.Accent, Thickness = 1}, toast)

    toast.BackgroundTransparency = 1
    toast.TextTransparency = 1
    TweenService:Create(toast, TweenInfo.new(0.2), {
        BackgroundTransparency = 0,
        TextTransparency = 0,
    }):Play()

    task.delay(2.5, function()
        if toast.Parent then
            local fade = TweenService:Create(toast, TweenInfo.new(0.2), {
                BackgroundTransparency = 1,
                TextTransparency = 1,
            })
            fade:Play()
            fade.Completed:Wait()
            toast:Destroy()
        end
    end)
end

-- Janela principal.
