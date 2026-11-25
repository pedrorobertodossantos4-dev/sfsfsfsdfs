
--================================
--       AQUA HUB V1.0
--       BLOX FRUITS
--================================

local Players = game:GetService("Players")
local player = Players.LocalPlayer

local gui = Instance.new("ScreenGui")
gui.Name = "AquaHub"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local main = Instance.new("Frame")
main.Size = UDim2.new(0, 500, 0, 350)
main.Position = UDim2.new(0.5, -250, 0.5, -175)
main.BackgroundColor3 = Color3.fromRGB(13, 18, 30)
main.BorderSizePixel = 0
main.Active = true
main.Draggable = true
main.Parent = gui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = main

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 55)
title.BackgroundColor3 = Color3.fromRGB(0, 115, 210)
title.Text = "AQUA HUB  |  V1.0"
title.TextColor3 = Color3.new(1,1,1)
title.Font = Enum.Font.GothamBold
title.TextSize = 23
title.Parent = main

local tabs = {
    "Auto Farm",
    "Sea",
    "ESP",
    "Hunter",
    "Config"
}

local states = {}

local content = Instance.new("Frame")
content.Position = UDim2.new(0, 150, 0, 65)
content.Size = UDim2.new(1, -165, 1, -80)
content.BackgroundTransparency = 1
content.Parent = main

local function createButton(parent, name, y)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, -10, 0, 40)
    button.Position = UDim2.new(0, 5, 0, y)
    button.BackgroundColor3 = Color3.fromRGB(30, 43, 65)
    button.TextColor3 = Color3.new(1,1,1)
    button.Font = Enum.Font.GothamBold
    button.TextSize = 14
    button.Text = name .. ": OFF"
    button.Parent = parent

    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 7)
    c.Parent = button

    states[name] = false

    button.MouseButton1Click:Connect(function()
        states[name] = not states[name]

        button.Text = name .. ": " ..
            (states[name] and "ON" or "OFF")

        button.BackgroundColor3 = states[name]
            and Color3.fromRGB(0, 130, 90)
            or Color3.fromRGB(30, 43, 65)
    end)
end

local function showTab(tab)
    content:ClearAllChildren()

    if tab == "Auto Farm" then
        createButton(content, "Auto Farm", 10)
        createButton(content, "Auto Quest", 60)
        createButton(content, "Auto M1", 110)

    elseif tab == "Sea" then
        createButton(content, "Sea Events", 10)
        createButton(content, "Sea Farm", 60)
        createButton(content, "Fruit Farm", 110)

    elseif tab == "ESP" then
        createButton(content, "Player ESP", 10)
        createButton(content, "Chest ESP", 60)
        createButton(content, "Enemy ESP", 110)

    elseif tab == "Hunter" then
        createButton(content, "Elite Hunter", 10)

    elseif tab == "Config" then
        createButton(content, "Show Settings", 10)
    end
end

for i, tab in ipairs(tabs) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 130, 0, 42)
    button.Position = UDim2.new(0, 10, 0, 65 + (i-1)*49)
    button.BackgroundColor3 = Color3.fromRGB(24, 40, 62)
    button.TextColor3 = Color3.new(1,1,1)
    button.Text = tab
    button.Font = Enum.Font.GothamBold
    button.TextSize = 13
    button.Parent = main

    button.MouseButton1Click:Connect(function()
        showTab(tab)
    end)
end

local close = Instance.new("TextButton")
close.Size = UDim2.new(0, 30, 0, 30)
close.Position = UDim2.new(1, -38, 0, 12)
close.BackgroundColor3 = Color3.fromRGB(180, 40, 50)
close.Text = "X"
close.TextColor3 = Color3.new(1,1,1)
close.Font = Enum.Font.GothamBold
close.Parent = main

close.MouseButton1Click:Connect(function()
    gui:Destroy()
end)

showTab("Auto Farm")

print("AQUA HUB V1.0 carregado!")
