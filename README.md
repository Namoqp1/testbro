local Fluent = loadstring(game:HttpGet("https://raw.githubusercontent.com/Namoqp1/dump/refs/heads/main/them"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/barlossxi/barlossxi/main/ZAZA.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/barlossxi/barlossxi/main/InterfaceManager.lua.txt"))()

local ScreenGui1 = Instance.new("ScreenGui")
local ImageButton1 = Instance.new("ImageButton")
local UICorner = Instance.new("UICorner")

ScreenGui1.Name = "ImageButton"
ScreenGui1.Parent = game.CoreGui
ScreenGui1.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

ImageButton1.Parent = ScreenGui1
ImageButton1.BackgroundTransparency = 1
ImageButton1.BorderSizePixel = 0
ImageButton1.Position = UDim2.new(0.120833337, 0, 0.0952890813, 0)
ImageButton1.Size = UDim2.new(0, 50, 0, 50)
ImageButton1.Draggable = true
ImageButton1.Image = "rbxassetid://10723396107"
ImageButton1.MouseButton1Down:Connect(function()
	game:GetService("VirtualInputManager"):SendKeyEvent(true,305,false,game)
	game:GetService("VirtualInputManager"):SendKeyEvent(false,305,false,game)
end)
UICorner.Parent = ImageButton1

local Window = Fluent:CreateWindow({
	Title = "Old Toilet TD",
	SubTitle = "ddcmmc",
	TabWidth = 130,
	Size = UDim2.fromOffset(480, 400),
	Acrylic = false, 
	Theme = "Dark",
	MinimizeKey = Enum.KeyCode.RightControl
})

local Tabs = {
	Setting = Window:AddTab({ Title = "Setting", Icon = "settings" })
}

local aza = "Work 5 Configs"
local bza = tostring(game.PlaceId).."-"..tostring(game.Players.LocalPlayer.Name)


local aza = "Ladius HUB Configs"
local bza = tostring(game.PlaceId).."-"..tostring(game.Players.LocalPlayer.Name)
function saveSettings()
	local cza = game:GetService("HttpService")
	local dza = cza:JSONEncode(_G)
	if writefile then
		if isfolder(aza) then
			if isfolder(bza) then
				writefile(aza .. "\\" .. bza, dza)
			else
				makefolder(aza .. "\\" .. bza)
			end
		else
			makefolder(aza)
		end
	end
end
function loadSettings()
	local cza = game:GetService("HttpService")
	if isfile(aza .. "\\" .. bza) then
		_G = cza:JSONDecode(readfile(aza .. "\\" .. bza))
	end
end
loadSettings()


Tabs.Setting:AddToggle("Host Bot", {
	Title = "Host Bot",
	Default = false,
	Callback = function(Host)
		_G.Host= Host
		saveSettings()
	end
})

spawn(function()
	while task.wait(5) do
		if _G.Host then
			pcall(function()
				print("Ez")
			end)
		end
	end
end)

