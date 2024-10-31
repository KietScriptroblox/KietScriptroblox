local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local frame = playerGui:WaitForChild("YourFrame")
local textBox = playerGui:WaitForChild("YourTextBox")
local button = playerGui:WaitForChild("YourButton")

local titleLabel = Instance.new("TextLabel")
titleLabel.Text = "Kiet-Mod"
titleLabel.Size = UDim2.new(1, 0, 0, 50)
titleLabel.Position = UDim2.new(0, 0, 0, 0)
titleLabel.Parent = frame

local dragging = false
local dragInput
local dragStart
local startPos

frame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = frame.Position
    end
end)

frame.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)

game:GetService("UserInputService").InputChanged:Connect(function(input)
    if dragging then
        local delta = input.Position - dragStart
        frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

button.MouseButton1Click:Connect(function()
    local inputValue = tonumber(textBox.Text)
    if inputValue then
        local bountyReceived = inputValue
        print("You received " .. bountyReceived .. " Bounty!")
    end
end)
