local UI = game:GetObjects("rbxassetid://8524217009")[1]
if game.CoreGui:FindFirstChild("FPSCounter") then
	game.CoreGui:FindFirstChild("FPSCounter"):Destroy()
end
UI.Parent = game.CoreGui
UI.Main.Position = UDim2.new(0, 959,0, 49)
print(UI.Main.Position)
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local DR = false

if isfile and readfile then
	local YOffset = 49
	local XOffset = 959
	if isfile("FPS Position Y Offset.txt") then
		YOffset = readfile("FPS Position Y Offset.txt")
	end
	if isfile("FPS Position X Offset.txt") then
		XOffset = readfile("FPS Position X Offset.txt")
	end
	
	local Position = UDim2.new(0,XOffset,0,YOffset)
	UI.Main.Position = Position
end

UI.Main.BackgroundTransparency = 1
UI.Main.Title.TextTransparency = 1

local transitionInfo = TweenInfo.new(0.8, Enum.EasingStyle.Back)
local tween = TweenService:Create(UI.Main, transitionInfo, {BackgroundTransparency = 0.8})
tween:Play()
local transitionInfo = TweenInfo.new(0.8, Enum.EasingStyle.Back)
local tween = TweenService:Create(UI.Main.Title, transitionInfo, {TextTransparency = 0.4})
tween:Play()


local function MakeDraggable(objecttodragfrom, object) 
	pcall(function()
		local dragging = false
		local dragInput, mousePos, framePos

		objecttodragfrom.InputBegan:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 then
				dragging = true
				DR = true
				mousePos = input.Position
				framePos = object.Position

				input.Changed:Connect(function()
					if input.UserInputState == Enum.UserInputState.End then
						dragging = false
					end
				end)
			end
		end)

		objecttodragfrom.InputChanged:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseMovement then
				dragInput = input
			end
		end)

		UserInputService.InputChanged:Connect(function(input)
			if input == dragInput and dragging then
				local delta = input.Position - mousePos
				local transitionInfo = TweenInfo.new(0.4, Enum.EasingStyle.Quint)
				local tween = TweenService:Create(object, transitionInfo, {Position = UDim2.new(0, framePos.X.Offset + delta.X, 0, framePos.Y.Offset + delta.Y)})
				tween:Play()
				wait(0.1)
			end
		end)
	end)
end

MakeDraggable(UI.Main,UI.Main)

UI.Main.MouseEnter:Connect(function()
	local transitionInfo = TweenInfo.new(0.8, Enum.EasingStyle.Quint)
	local tween = TweenService:Create(UI.Main, transitionInfo, {BackgroundTransparency = 0.4})
	tween:Play()
	local transitionInfo = TweenInfo.new(0.8, Enum.EasingStyle.Quint)
	local tween = TweenService:Create(UI.Main.Title, transitionInfo, {TextTransparency = 0.1})
	tween:Play()
end)

UI.Main.MouseLeave:Connect(function()
	local transitionInfo = TweenInfo.new(0.8, Enum.EasingStyle.Quint)
	local tween = TweenService:Create(UI.Main, transitionInfo, {BackgroundTransparency = 0.8})
	tween:Play()
	local transitionInfo = TweenInfo.new(0.8, Enum.EasingStyle.Quint)
	local tween = TweenService:Create(UI.Main.Title, transitionInfo, {TextTransparency = 0.4})
	tween:Play()
end)


local FPSLabel = UI.Main.Title
local Heartbeat = game:GetService("RunService").Heartbeat

local LastIteration, Start
local FrameUpdateTable = { }

local function HeartbeatUpdate()
	LastIteration = tick()
	for Index = #FrameUpdateTable, 1, -1 do
		FrameUpdateTable[Index + 1] = (FrameUpdateTable[Index] >= LastIteration - 1) and FrameUpdateTable[Index] or nil
	end
	FrameUpdateTable[1] = LastIteration
	local CurrentFPS = (tick() - Start >= 1 and #FrameUpdateTable) or (#FrameUpdateTable / (tick() - Start))
	CurrentFPS = math.floor(CurrentFPS)
	
	FPSLabel.Text = tostring(CurrentFPS).." FPS"
end

Start = tick()
Heartbeat:Connect(HeartbeatUpdate)


while true do
	wait(2)
	writefile("FPS Position Y Offset.txt",UI.Main.Position.Y.Offset)
	writefile("FPS Position X Offset.txt",UI.Main.Position.X.Offset)
end
