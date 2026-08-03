local Players = game:GetService("Players")
local player = Players.LocalPlayer

local gui = Instance.new("ScreenGui")
gui.Name = "CustomUI"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

-- Khung chính
local main = Instance.new("Frame")
main.Parent = gui
main.Size = UDim2.new(0, 850, 0, 450)
main.Position = UDim2.new(0.5, -425, 0.5, -225)
main.BackgroundColor3 = Color3.fromRGB(35,35,35)
main.BorderSizePixel = 0

local corner = Instance.new("UICorner", main)
corner.CornerRadius = UDim.new(0,15)

-- Panel trái
local left = Instance.new("Frame")
left.Parent = main
left.Size = UDim2.new(0,250,1,0)
left.BackgroundColor3 = Color3.fromRGB(45,45,45)
left.BorderSizePixel = 0

local leftCorner = Instance.new("UICorner", left)
leftCorner.CornerRadius = UDim.new(0,15)

-- Đường phân cách
local line = Instance.new("Frame")
line.Parent = main
line.Position = UDim2.new(0,250,0,0)
line.Size = UDim2.new(0,2,1,0)
line.BackgroundColor3 = Color3.fromRGB(70,70,70)
line.BorderSizePixel = 0

-- Panel phải
local right = Instance.new("Frame")
right.Parent = main
right.Position = UDim2.new(0,252,0,0)
right.Size = UDim2.new(1,-252,1,0)
right.BackgroundColor3 = Color3.fromRGB(40,40,40)
right.BorderSizePixel = 0

-- Nút Unlock
local unlock = Instance.new("TextButton")
unlock.Parent = gui
unlock.Size = UDim2.new(0,160,0,55)
unlock.Position = UDim2.new(0,20,0,40)
unlock.Text = "Unlock"
unlock.Font = Enum.Font.GothamBold
unlock.TextSize = 28
unlock.BackgroundColor3 = Color3.fromRGB(255,255,255)
unlock.TextColor3 = Color3.fromRGB(0,0,0)
Instance.new("UICorner", unlock).CornerRadius = UDim.new(0,12)

-- Nút Toggle
local toggle = Instance.new("TextButton")
toggle.Parent = gui
toggle.Size = UDim2.new(0,160,0,55)
toggle.Position = UDim2.new(0,20,0,110)
toggle.Text = "TOGGLE"
toggle.Font = Enum.Font.GothamBold
toggle.TextSize = 24
toggle.BackgroundColor3 = Color3.fromRGB(255,255,255)
toggle.TextColor3 = Color3.fromRGB(0,0,0)
Instance.new("UICorner", toggle).CornerRadius = UDim.new(0,12)

-- Nút kéo UI
local drag = Instance.new("TextButton")
drag.Parent = main
drag.Size = UDim2.new(0,50,0,50)
drag.Position = UDim2.new(1,-60,0,10)
drag.Text = "✥"
drag.Font = Enum.Font.GothamBold
drag.TextSize = 26
drag.BackgroundColor3 = Color3.fromRGB(255,255,255)
drag.TextColor3 = Color3.fromRGB(0,0,0)
Instance.new("UICorner", drag).CornerRadius = UDim.new(0,10)

-- Toggle hiện/ẩn
toggle.MouseButton1Click:Connect(function()
	main.Visible = not main.Visible
end)

-- Unlock (ví dụ)
unlock.MouseButton1Click:Connect(function()
	print("Unlock Clicked")
end)

-- Kéo UI
local UIS = game:GetService("UserInputService")

local dragging = false
local dragStart
local startPos

drag.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = main.Position

		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

UIS.InputChanged:Connect(function(input)
	if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local delta = input.Position - dragStart
		main.Position = UDim2.new(
			startPos.X.Scale,
			startPos.X.Offset + delta.X,
			startPos.Y.Scale,
			startPos.Y.Offset + delta.Y
		)
	end
end)
