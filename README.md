local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")

local player = Players.LocalPlayer
local gui = Instance.new("ScreenGui")
gui.Name = "PinkPanel"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local image = Instance.new("ImageLabel")
image.Name = "PinkImage"
image.Parent = gui
image.Size = UDim2.fromOffset(460, 215)
image.Position = UDim2.new(0.5, -230, 0.3, 0)
image.BackgroundTransparency = 1
image.Image = "<img width="1774" height="887" alt="515362C9-5551-4866-8E95-65DAD00670B2" src="https://github.com/user-attachments/assets/c12d869c-02a4-43ab-9fb9-9f7b844edc64" />
"
image.ScaleType = Enum.ScaleType.Fit
image.Active = true

-- Закруглённые края
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 25)
corner.Parent = image

-- Перемещение мышкой и пальцем
local dragging = false
local dragStart
local startPos

image.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1
    or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = image.Position
    end
end)

UIS.InputChanged:Connect(function(input)
    if dragging and (
        input.UserInputType == Enum.UserInputType.MouseMovement
        or input.UserInputType == Enum.UserInputType.Touch
    ) then
        local delta = input.Position - dragStart
        image.Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
    end
end)

UIS.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1
    or input.UserInputType == Enum.UserInputType.Touch then
        dragging = false
    end
end)
