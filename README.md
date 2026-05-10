--// S2 WOOD HUB V3
--// Hub com abas

local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local hum = char:WaitForChild("Humanoid")

-- GUI
local gui = Instance.new("ScreenGui")
gui.Name = "S2WOODHUB"
gui.Parent = player.PlayerGui

-- MAIN
local main = Instance.new("Frame")
main.Parent = gui
main.Size = UDim2.new(0,650,0,400)
main.Position = UDim2.new(0.25,0,0.2,0)
main.BackgroundColor3 = Color3.fromRGB(12,12,12)
main.Active = true
main.Draggable = true

Instance.new("UICorner",main).CornerRadius = UDim.new(0,15)

local stroke = Instance.new("UIStroke")
stroke.Parent = main
stroke.Color = Color3.fromRGB(255,0,0)
stroke.Thickness = 2

-- TOPBAR
local top = Instance.new("Frame")
top.Parent = main
top.Size = UDim2.new(1,0,0,45)
top.BackgroundColor3 = Color3.fromRGB(20,20,20)

Instance.new("UICorner",top).CornerRadius = UDim.new(0,15)

local title = Instance.new("TextLabel")
title.Parent = top
title.Size = UDim2.new(1,0,1,0)
title.BackgroundTransparency = 1
title.Text = "S2 WOOD HUB"
title.TextColor3 = Color3.new(1,1,1)
title.TextScaled = true

-- SIDEBAR
local side = Instance.new("Frame")
side.Parent = main
side.Size = UDim2.new(0,150,1,-45)
side.Position = UDim2.new(0,0,0,45)
side.BackgroundColor3 = Color3.fromRGB(18,18,18)

-- PAGES
local pages = Instance.new("Folder")
pages.Name = "Pages"
pages.Parent = main

local function CreatePage(name)

	local page = Instance.new("Frame")
	page.Name = name
	page.Parent = pages
	page.Size = UDim2.new(1,-160,1,-55)
	page.Position = UDim2.new(0,155,0,50)
	page.BackgroundTransparency = 1
	page.Visible = false

	local layout = Instance.new("UIListLayout")
	layout.Parent = page
	layout.Padding = UDim.new(0,10)

	return page
end

local playerPage = CreatePage("Player")
local trollPage = CreatePage("Troll")
local miscPage = CreatePage("Misc")

playerPage.Visible = true

-- BOTÕES DAS ABAS
local function TabButton(name,pos,page)

	local btn = Instance.new("TextButton")
	btn.Parent = side
	btn.Size = UDim2.new(0,130,0,40)
	btn.Position = UDim2.new(0,10,0,pos)
	btn.Text = name
	btn.BackgroundColor3 = Color3.fromRGB(25,25,25)
	btn.TextColor3 = Color3.new(1,1,1)

	Instance.new("UICorner",btn).CornerRadius = UDim.new(0,10)

	btn.MouseButton1Click:Connect(function()

		for _,v in pairs(pages:GetChildren()) do
			v.Visible = false
		end

		page.Visible = true

	end)

end

TabButton("Player",20,playerPage)
TabButton("Troll",70,trollPage)
TabButton("Misc",120,miscPage)

-- BOTÕES INTERNOS
local function CreateButton(parent,name,callback)

	local btn = Instance.new("TextButton")
	btn.Parent = parent
	btn.Size = UDim2.new(0,420,0,45)
	btn.Text = name
	btn.BackgroundColor3 = Color3.fromRGB(25,25,25)
	btn.TextColor3 = Color3.new(1,1,1)

	Instance.new("UICorner",btn).CornerRadius = UDim.new(0,12)

	local s = Instance.new("UIStroke")
	s.Parent = btn
	s.Color = Color3.fromRGB(255,0,0)

	btn.MouseButton1Click:Connect(callback)

end

-- PLAYER TAB
CreateButton(playerPage,"Speed",function()
	hum.WalkSpeed = 50
end)

CreateButton(playerPage,"Super Jump",function()
	hum.JumpPower = 120
end)

CreateButton(playerPage,"Invisible",function()

	for _,v in pairs(char:GetDescendants()) do
		if v:IsA("BasePart") then
			v.Transparency = 1
		end
	end

end)

-- TROLL TAB
CreateButton(trollPage,"Big Head",function()

	if char:FindFirstChild("Head") then
		char.Head.Size = Vector3.new(5,5,5)
	end

end)

CreateButton(trollPage,"RGB Body",function()

	while true do
		task.wait(0.2)

		for _,p in pairs(char:GetChildren()) do
			if p:IsA("BasePart") then

				p.Color = Color3.fromRGB(
					math.random(0,255),
					math.random(0,255),
					math.random(0,255)
				)

			end
		end
	end

end)

CreateButton(trollPage,"Spin",function()

	while true do
		task.wait()

		if char:FindFirstChild("HumanoidRootPart") then
			char.HumanoidRootPart.CFrame *= CFrame.Angles(0,math.rad(20),0)
		end
	end

end)

-- MISC TAB
CreateButton(miscPage,"Low Gravity",function()
	workspace.Gravity = 50
end)

CreateButton(miscPage,"Normal Gravity",function()
	workspace.Gravity = 196.2
end)

CreateButton(miscPage,"Destroy GUI",function()
	gui:Destroy()
end)
