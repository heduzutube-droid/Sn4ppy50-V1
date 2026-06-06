# Sn4ppy50-V1
A script what works for delta roblox script
heres the script
-- Snapping V1 - CHUNK 1

local Players = game:GetService("Players")
local Lighting = game:GetService("Lighting")
local UIS = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local oldGui = playerGui:FindFirstChild("SN4PPY50_V1")
if oldGui then
	oldGui:Destroy()
end

local gui = Instance.new("ScreenGui")
gui.Name = "SN4PPY50_V1"
gui.ResetOnSpawn = false
gui.Parent = playerGui

local frame = Instance.new("ScrollingFrame")
frame.Size = UDim2.new(0, 520, 0, 500)
frame.Position = UDim2.new(0, 50, 0, 50)
frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
frame.BorderSizePixel = 0
frame.CanvasSize = UDim2.new(0,0,0,3000)
frame.ScrollBarThickness = 8
frame.Parent = gui

Instance.new("UICorner", frame)

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1,0,0,40)
title.BackgroundColor3 = Color3.fromRGB(35,35,35)
title.Text = "SN4PPY50 V1"
title.TextScaled = true
title.TextColor3 = Color3.new(1,1,1)
title.Parent = frame

Instance.new("UICorner", title)

task.spawn(function()
	while title.Parent do
		for i = 0,1,0.01 do
			title.TextColor3 = Color3.fromHSV(i,1,1)
			task.wait(0.03)
		end
	end
end)

local dragging = false
local dragStart
local startPos

title.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = frame.Position
	end
end)

UIS.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = false
	end
end)

UIS.InputChanged:Connect(function(input)
	if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local delta = input.Position - dragStart

		frame.Position = UDim2.new(
			startPos.X.Scale,
			startPos.X.Offset + delta.X,
			startPos.Y.Scale,
			startPos.Y.Offset + delta.Y
		)
	end
end)

local col = 0
local row = 55

local function Button(text, callback)
	local b = Instance.new("TextButton")
	b.Size = UDim2.new(0,160,0,30)
	b.Position = UDim2.new(0,10 + (col * 170),0,row)
	b.BackgroundColor3 = Color3.fromRGB(45,45,45)
	b.TextColor3 = Color3.new(1,1,1)
	b.TextScaled = true
	b.Text = text
	b.Parent = frame

	Instance.new("UICorner", b)

	b.MouseButton1Click:Connect(callback)

	col += 1

	if col >= 3 then
		col = 0
		row += 40
	end

	frame.CanvasSize = UDim2.new(0,0,0,row + 200)
end

local function Hum()
	local c = player.Character
	if c then
		return c:FindFirstChildOfClass("Humanoid")
	end
end
Button("Night", function()
	Lighting.ClockTime = 0
end)

Button("Day", function()
	Lighting.ClockTime = 14
end)

Button("Low Gravity", function()
	workspace.Gravity = 50
end)

Button("Normal Gravity", function()
	workspace.Gravity = 196.2
end)

Button("Speed+", function()
	local h = Hum()
	if h then
		h.WalkSpeed = 50
	end
end)

Button("Speed Reset", function()
	local h = Hum()
	if h then
		h.WalkSpeed = 16
	end
end)

Button("Jump+", function()
	local h = Hum()
	if h then
		h.JumpPower = 100
	end
end)

Button("Jump Reset", function()
	local h = Hum()
	if h then
		h.JumpPower = 50
	end
end)

Button("Big Head", function()
	local c = player.Character
	if c and c:FindFirstChild("Head") then
		c.Head.Size = Vector3.new(3,3,3)
	end
end)

Button("Small Head", function()
	local c = player.Character
	if c and c:FindFirstChild("Head") then
		c.Head.Size = Vector3.new(1,1,1)
	end
end)

Button("Sparkles", function()
	local c = player.Character
	if not c then return end

	for _,v in ipairs(c:GetChildren()) do
		if v:IsA("BasePart") then
			Instance.new("Sparkles", v)
		end
	end
end)

Button("Remove Sparkles", function()
	local c = player.Character
	if not c then return end

	for _,v in ipairs(c:GetDescendants()) do
		if v:IsA("Sparkles") then
			v:Destroy()
		end
	end
end)

Button("Rainbow Me", function()
	local c = player.Character
	if not c then return end

	task.spawn(function()
		for i=1,200 do
			local clr = Color3.fromHSV(i/200,1,1)

			for _,v in ipairs(c:GetDescendants()) do
				if v:IsA("BasePart") then
					v.Color = clr
				end
			end

			task.wait(0.03)
		end
	end)
end)

Button("Hello", function()
	print("Hi!")
end)

Button("Spin Me", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	task.spawn(function()
		for i=1,100 do
			root.CFrame *= CFrame.Angles(0, math.rad(15), 0)
			task.wait()
		end
	end)
end)
-- VISUAL / WORLD BUTTONS

Button("Fog On", function()
	Lighting.FogEnd = 50
end)

Button("Fog Off", function()
	Lighting.FogEnd = 100000
end)

Button("Red Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(150,30,30)
end)

Button("Blue Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(30,60,180)
end)

Button("Green Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(30,150,30)
end)

Button("Purple Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(120,50,180)
end)

Button("Dark Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
end)

Button("RGB GUI", function()
	task.spawn(function()
		for i = 1,300 do
			frame.BackgroundColor3 = Color3.fromHSV(i/300,1,1)
			task.wait(0.02)
		end
	end)
end)

Button("RGB Title", function()
	task.spawn(function()
		for i = 1,300 do
			title.TextColor3 = Color3.fromHSV(i/300,1,1)
			task.wait(0.02)
		end
	end)
end)

Button("Blur Vision", function()
	local blur = Lighting:FindFirstChild("SNBlur")

	if not blur then
		blur = Instance.new("BlurEffect")
		blur.Name = "SNBlur"
		blur.Parent = Lighting
	end

	blur.Size = 24
end)

Button("Clear Blur", function()
	local blur = Lighting:FindFirstChild("SNBlur")

	if blur then
		blur.Size = 0
	end
end)

Button("Zoom FOV", function()
	workspace.CurrentCamera.FieldOfView = 100
end)

Button("Normal FOV", function()
	workspace.CurrentCamera.FieldOfView = 70
end)

Button("Disco Lights", function()
	task.spawn(function()
		for i = 1,100 do
			Lighting.Ambient = Color3.fromHSV(math.random(),1,1)
			task.wait(0.05)
		end

		Lighting.Ambient = Color3.fromRGB(128,128,128)
	end)
end)

Button("Neon World", function()
	for _,v in ipairs(workspace:GetDescendants()) do
		if v:IsA("BasePart") then
			v.Material = Enum.Material.Neon
		end
	end
end)

Button("Black World", function()
	for _,v in ipairs(workspace:GetDescendants()) do
		if v:IsA("BasePart") then
			v.Color = Color3.new(0,0,0)
		end
	end
end)

Button("White World", function()
	for _,v in ipairs(workspace:GetDescendants()) do
		if v:IsA("BasePart") then
			v.Color = Color3.new(1,1,1)
		end
	end
end)

Button("Random Colors", function()
	for _,v in ipairs(workspace:GetDescendants()) do
		if v:IsA("BasePart") then
			v.Color = Color3.fromHSV(math.random(),1,1)
		end
	end
end)

Button("Bright World", function()
	Lighting.Brightness = 5
end)

Button("Normal Brightness", function()
	Lighting.Brightness = 2
end)

Button("Sunset", function()
	Lighting.ClockTime = 18
end)

Button("Midnight", function()
	Lighting.ClockTime = 0
end)

Button("Morning", function()
	Lighting.ClockTime = 8
end)

Button("Storm Mode", function()
	Lighting.FogEnd = 75
	Lighting.Brightness = 1
	Lighting.ClockTime = 22
end)

Button("Flash Screen", function()
	task.spawn(function()
		for i = 1,10 do
			frame.BackgroundColor3 = Color3.new(1,1,1)
			task.wait(0.05)
			frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
			task.wait(0.05)
		end
	end)
end)

Button("Rainbow Ambient", function()
	task.spawn(function()
		for i = 1,300 do
			Lighting.Ambient = Color3.fromHSV(i/300,1,1)
			task.wait(0.03)
		end
	end)
end)

Button("Pink Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(255,105,180)
end)

Button("Orange Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(255,140,0)
end)

Button("Cyan Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(0,255,255)
end)

Button("Reset Visuals", function()
	Lighting.ClockTime = 14
	Lighting.FogEnd = 100000
	Lighting.Brightness = 2
	workspace.CurrentCamera.FieldOfView = 70

	frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
	title.TextColor3 = Color3.new(1,1,1)
end)
-- FUN / TROLL / PARTICLE BUTTONS

Button("Fireworks", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local p = Instance.new("Part")
	p.Anchored = true
	p.Transparency = 1
	p.Position = root.Position + Vector3.new(0,20,0)
	p.Parent = workspace

	local emitter = Instance.new("ParticleEmitter")
	emitter.Rate = 500
	emitter.Speed = NumberRange.new(15)
	emitter.Lifetime = NumberRange.new(2)
	emitter.Parent = p

	task.delay(3,function()
		p:Destroy()
	end)
end)

Button("Confetti", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local p = Instance.new("ParticleEmitter")
	p.Texture = "rbxasset://textures/particles/sparkles_main.dds"
	p.Rate = 400
	p.Lifetime = NumberRange.new(2)
	p.Speed = NumberRange.new(10)
	p.Parent = root

	task.delay(3,function()
		p:Destroy()
	end)
end)

Button("Floating Cubes", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	for i = 1,20 do
		local cube = Instance.new("Part")
		cube.Size = Vector3.new(2,2,2)
		cube.Anchored = true
		cube.Material = Enum.Material.Neon
		cube.Color = Color3.fromHSV(math.random(),1,1)

		cube.Position = root.Position + Vector3.new(
			math.random(-20,20),
			math.random(5,15),
			math.random(-20,20)
		)

		cube.Parent = workspace
	end
end)

Button("Spawn Ball", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local ball = Instance.new("Part")
	ball.Shape = Enum.PartType.Ball
	ball.Size = Vector3.new(5,5,5)
	ball.Position = root.Position + Vector3.new(0,10,0)
	ball.Parent = workspace
end)

Button("Rainbow Balls", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	for i = 1,10 do
		local ball = Instance.new("Part")
		ball.Shape = Enum.PartType.Ball
		ball.Size = Vector3.new(3,3,3)
		ball.Color = Color3.fromHSV(i/10,1,1)
		ball.Position = root.Position + Vector3.new(
			math.random(-15,15),
			10,
			math.random(-15,15)
		)
		ball.Parent = workspace
	end
end)

Button("Meteor Shower", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	for i = 1,15 do
		local meteor = Instance.new("Part")
		meteor.Shape = Enum.PartType.Ball
		meteor.Size = Vector3.new(5,5,5)
		meteor.Material = Enum.Material.Neon
		meteor.Color = Color3.fromRGB(255,120,0)

		meteor.Position = root.Position + Vector3.new(
			math.random(-100,100),
			80,
			math.random(-100,100)
		)

		meteor.Parent = workspace
	end
end)

Button("Spin GUI", function()
	local tween = TweenService:Create(
		frame,
		TweenInfo.new(1),
		{Rotation = 5}
	)
	tween:Play()
end)

Button("Shake GUI", function()
	local original = frame.Position

	task.spawn(function()
		for i = 1,20 do
			frame.Position = original + UDim2.new(
				0, math.random(-10,10),
				0, math.random(-10,10)
			)
			task.wait(0.03)
		end

		frame.Position = original
	end)
end)

Button("Fake Error", function()
	warn("SN4PPY50 ERROR: Totally fake error.")
end)

Button("Print Spam", function()
	for i = 1,50 do
		print("SN4PPY50 "..i)
	end
end)

Button("Rainbow Frame", function()
	task.spawn(function()
		for i = 1,500 do
			frame.BackgroundColor3 = Color3.fromHSV(i/500,1,1)
			task.wait(0.02)
		end
	end)
end)

Button("Big Cube", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local p = Instance.new("Part")
	p.Size = Vector3.new(20,20,20)
	p.Position = root.Position + Vector3.new(0,15,0)
	p.Parent = workspace
end)

Button("Platform", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local p = Instance.new("Part")
	p.Size = Vector3.new(20,1,20)
	p.Anchored = true
	p.Position = root.Position - Vector3.new(0,4,0)
	p.Parent = workspace
end)

Button("Neon Platform", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local p = Instance.new("Part")
	p.Size = Vector3.new(20,1,20)
	p.Anchored = true
	p.Material = Enum.Material.Neon
	p.Color = Color3.fromHSV(math.random(),1,1)
	p.Position = root.Position - Vector3.new(0,4,0)
	p.Parent = workspace
end)

Button("Hello World", function()
	print("Hello World!")
end)

Button("Random Theme", function()
	frame.BackgroundColor3 = Color3.fromHSV(math.random(),1,1)
end)

Button("Rainbow Theme", function()
	task.spawn(function()
		for i = 1,300 do
			frame.BackgroundColor3 = Color3.fromHSV(i/300,1,1)
			task.wait(0.03)
		end
	end)
end)

Button("Reset GUI Color", function()
	frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
end)
Button("Tiny Character", function()
	local hum = Hum()
	if hum then
		hum.BodyHeightScale.Value = 0.5
		hum.BodyWidthScale.Value = 0.5
		hum.BodyDepthScale.Value = 0.5
	end
end)

Button("Giant Character", function()
	local hum = Hum()
	if hum then
		hum.BodyHeightScale.Value = 1.5
		hum.BodyWidthScale.Value = 1.5
		hum.BodyDepthScale.Value = 1.5
	end
end)

Button("Super Jump", function()
	local hum = Hum()
	if hum then
		hum.JumpPower = 200
	end
end)

Button("Walk On Air", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local p = Instance.new("Part")
	p.Size = Vector3.new(10,1,10)
	p.Anchored = true
	p.Position = root.Position - Vector3.new(0,4,0)
	p.Parent = workspace
end)

Button("Random Sky Color", function()
	Lighting.Ambient = Color3.fromHSV(math.random(),1,1)
end)

Button("Camera Zoom Max", function()
	player.CameraMaxZoomDistance = 500
end)

Button("Camera Zoom Reset", function()
	player.CameraMaxZoomDistance = 15
end)

Button("Flashbang", function()
	local blur = Instance.new("BlurEffect")
	blur.Size = 56
	blur.Parent = Lighting

	task.delay(2,function()
		blur:Destroy()
	end)
end)

Button("Spawn 50 Cubes", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	for i = 1,50 do
		local p = Instance.new("Part")
		p.Size = Vector3.new(2,2,2)
		p.Position = root.Position + Vector3.new(
			math.random(-30,30),
			math.random(5,30),
			math.random(-30,30)
		)
		p.Parent = workspace
	end
end)

Button("Rainbow Ambient", function()
	task.spawn(function()
		for i = 1,500 do
			Lighting.Ambient = Color3.fromHSV(i/500,1,1)
			task.wait(0.02)
		end
	end)
end)
-- CHUNK 6

Button("Dance Spin", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	task.spawn(function()
		for i = 1,120 do
			root.CFrame = root.CFrame * CFrame.Angles(0, math.rad(15), 0)
			task.wait()
		end
	end)
end)

Button("Moon Mode", function()
	workspace.Gravity = 30
end)

Button("Earth Mode", function()
	workspace.Gravity = 196.2
end)

Button("Bright Lights", function()
	Lighting.Brightness = 10
end)

Button("Normal Lights", function()
	Lighting.Brightness = 2
end)

Button("Blue Sky", function()
	Lighting.Ambient = Color3.fromRGB(100,150,255)
end)

Button("Red Sky", function()
	Lighting.Ambient = Color3.fromRGB(255,80,80)
end)

Button("Green Sky", function()
	Lighting.Ambient = Color3.fromRGB(80,255,80)
end)

Button("Rainbow Sky", function()
	task.spawn(function()
		for i = 1,400 do
			Lighting.Ambient = Color3.fromHSV(i/400,1,1)
			task.wait(0.02)
		end
	end)
end)

Button("Spawn Tower", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	for i = 1,15 do
		local p = Instance.new("Part")
		p.Size = Vector3.new(4,4,4)
		p.Position = root.Position + Vector3.new(15,i*4,0)
		p.Parent = workspace
	end
end)

Button("Spawn Rainbow Tower", function()
	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end

	for i = 1,15 do
		local p = Instance.new("Part")
		p.Size = Vector3.new(4,4,4)
		p.Color = Color3.fromHSV(i/15,1,1)
		p.Material = Enum.Material.Neon
		p.Position = root.Position + Vector3.new(-15,i*4,0)
		p.Parent = workspace
	end
end)

Button("Fire Character", function()
	local char = player.Character
	if not char then return end

	for _,v in ipairs(char:GetChildren()) do
		if v:IsA("BasePart") then
			local fire = Instance.new("Fire")
			fire.Parent = v
		end
	end
end)

Button("Remove Fire", function()
	local char = player.Character
	if not char then return end

	for _,v in ipairs(char:GetDescendants()) do
		if v:IsA("Fire") then
			v:Destroy()
		end
	end
end)

Button("Smoke Character", function()
	local char = player.Character
	if not char then return end

	for _,v in ipairs(char:GetChildren()) do
		if v:IsA("BasePart") then
			local smoke = Instance.new("Smoke")
			smoke.Parent = v
		end
	end
end)

Button("Remove Smoke", function()
	local char = player.Character
	if not char then return end

	for _,v in ipairs(char:GetDescendants()) do
		if v:IsA("Smoke") then
			v:Destroy()
		end
	end
end)

Button("Random WalkSpeed", function()
	local hum = Hum()
	if hum then
		hum.WalkSpeed = math.random(10,150)
	end
end)

Button("Random Jump", function()
	local hum = Hum()
	if hum then
		hum.JumpPower = math.random(50,250)
	end
end)

Button("Random Gravity", function()
	workspace.Gravity = math.random(20,300)
end)

Button("Reset Player", function()
	local hum = Hum()
	if hum then
		hum.WalkSpeed = 16
		hum.JumpPower = 50
	end

	workspace.Gravity = 196.2
end)
-- CHUNK 7

Button("Pink Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(255,105,180)
end)

Button("Orange Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(255,140,0)
end)

Button("Cyan Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(0,255,255)
end)

Button("Gold Theme", function()
	frame.BackgroundColor3 = Color3.fromRGB(255,215,0)
end)

Button("Tiny FOV", function()
	workspace.CurrentCamera.FieldOfView = 30
end)

Button("Huge FOV", function()
	workspace.CurrentCamera.FieldOfView = 120
end)

Button("Random FOV", function()
	workspace.CurrentCamera.FieldOfView = math.random(30,120)
end)

Button("Spawn Neon Cube", function()
	local p = Instance.new("Part")
	p.Size = Vector3.new(6,6,6)
	p.Material = Enum.Material.Neon
	p.Color = Color3.fromHSV(math.random(),1,1)
	p.Parent = workspace
end)

Button("Spawn Giant Ball", function()
	local b = Instance.new("Part")
	b.Shape = Enum.PartType.Ball
	b.Size = Vector3.new(15,15,15)
	b.Parent = workspace
end)

Button("Spawn Pyramid", function()
	for i = 1,5 do
		local p = Instance.new("Part")
		p.Size = Vector3.new(12-i*2,2,12-i*2)
		p.Position = Vector3.new(0,i*2,0)
		p.Parent = workspace
	end
end)

Button("Rainbow Parts", function()
	for _,v in ipairs(workspace:GetDescendants()) do
		if v:IsA("BasePart") then
			v.Color = Color3.fromHSV(math.random(),1,1)
		end
	end
end)

Button("Invisible Character", function()
	local char = player.Character
	if not char then return end

	for _,v in ipairs(char:GetDescendants()) do
		if v:IsA("BasePart") then
			v.Transparency = 1
		end
	end
end)

Button("Visible Character", function()
	local char = player.Character
	if not char then return end

	for _,v in ipairs(char:GetDescendants()) do
		if v:IsA("BasePart") then
			v.Transparency = 0
		end
	end
end)

Button("Rainbow Head", function()
	local char = player.Character
	if not char then return end

	local head = char:FindFirstChild("Head")
	if not head then return end

	task.spawn(function()
		for i = 1,300 do
			head.Color = Color3.fromHSV(i/300,1,1)
			task.wait(0.02)
		end
	end)
end)

Button("Super Bright", function()
	Lighting.Brightness = 20
end)

Button("Dark World", function()
	Lighting.Brightness = 0
end)

Button("Random Brightness", function()
	Lig
