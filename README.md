if not game:IsLoaded() then game.Loaded:Wait() end

repeat task.wait() until game:GetService("Players")
repeat task.wait() until game:GetService("Players").LocalPlayer
repeat task.wait() until game:GetService("ReplicatedStorage")
repeat task.wait() until game:GetService("ReplicatedFirst")




local function checkLine(s)
	local a = 0
	for i in string.gmatch(s, "[^\n]+") do
		a = a+1
	end
	return a
end
local start = 1
local function addspace(a)
	local st = ""
	for i = 0,a*2 do
		st = st.." "
	end
	return st
end
local function usd(v,i)
	local turn

	if typeof(v) == "Axes" then
		turn = "Axes.new("..tostring(v)..")"
	elseif typeof(v) == "BrickColor" then
		turn = "BrickColor.new("..tostring(v)..")"
	elseif typeof(v) == "CFrame" then
		turn = "CFrame.new("..tostring(v)..")"
	elseif typeof(v) == "Vector3" then
		turn = "Vector3.new("..tostring(v)..")"
	elseif typeof(v) == "Color3" then
		if v.r<=1 and v.g<= 1 and v.b<= 1 and v.r >= 0 and v.g >= 0 and v.b >= 0 then
			local R = v.r * 255
			local G = v.g * 255
			local B = v.b * 255
			turn = 'Color3.fromRGB('..R..", "..G..", "..B..")"..'    --Color3.new('..tostring(v)..")"
		else
			turn = "Color Error"
		end
	elseif typeof(v) == "Instance" then
		turn = "game."..tostring(v:GetFullName())
	elseif typeof(v) == "Enum" then
		turn = tostring(v).."   -- Enum"
	else
		turn = tostring(typeof(v))..".new("..tostring(v)..")"
	end
	if i then
		if type(i) == "number" then 
			return '['..tostring(i)..']'.. " = "..tostring(turn)
		end
		return '["'..tostring(i)..'"]'.. " = "..tostring(turn)
	end
	return tostring(turn)
end

local convert
local startSpace = 1
function convert(v,i,a)
	if not a then
		a = startSpace    
	end
	if type(v) == "string" then
		if checkLine(v) >= 2 then
			if type(i) == "number" then 
				return '['..tostring(i)..']'.. " = "..'[['..tostring(v)..']]'
			end
			return '["'..tostring(i)..'"]'.. " = "..'[['..tostring(v)..']]'
		else
			if type(i) == "number" then 
				return '['..tostring(i)..']'.. " = "..'"'..tostring(v)..'"'
			end
			return '["'..tostring(i)..'"]'.. " = "..'"'..tostring(v)..'"'
		end
	elseif type(v) == "number" then
		if type(i) == "number" then 
			return '['..tostring(i)..']'.. " = "..tostring(v)
		end
		return '["'..tostring(i)..'"]'.. " = "..tostring(v)
	elseif type(v) == "boolean" then
		if type(i) == "number" then 
			return '['..tostring(i)..']'.. " = "..tostring(v)
		end
		return '["'..tostring(i)..'"]'.. " = "..tostring(v)
	elseif type(v) == "nil" then
		if type(i) == "number" then 
			return '['..tostring(i)..']'.. " = "..tostring(v)
		end
		return '["'..tostring(i)..'"]'.. " = nil"
	elseif type(v) == "function" then
		local Name = ""
		if debug.getinfo(v).name == "" then
			Name = tostring(v)
		else
			Name = debug.getinfo(v).name
		end
		if type(i) == "number" then 
			return '['..tostring(i)..']'.. " = "..'function()end  '..'--'.."[["..tostring(Name).."]]"
		end
		return '["'..tostring(i)..'"]'.. " = "..'function()end  '..'--'.."[["..tostring(Name).."]]"
	elseif type(v) == "userdata" or type(v) == "vector" then
		return usd(v,i)
	elseif type(v) == "table" then
		if i~= nil then
			if type(i) == "number" then
				stt = '['..tostring(i)..']'.." = "..'{'
			else
				stt = '["'..tostring(i)..'"]'.." = "..'{'
			end

		else
			stt = '{'
		end
		local count_table = 0
		for i,v in pairs(v) do
			count_table = count_table+1
			if count_table == 1 then
				stt = stt .. "\n" .. tostring(addspace(a)) .. tostring(convert(v, i, a + 1))
			else    
				stt = stt .. ",\n" .. tostring(addspace(a)) .. tostring(convert(v, i, a + 1))
			end
		end
		return stt.."\n}"
	elseif type(v) == "thread" then
		if type(i) == "number" then 
			return '['..tostring(i)..']'.. " = "..tostring(v)
		end
		return '["'..tostring(i)..'"]'.. " = "..tostring(v)
	end
end



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
	Setting = Window:AddTab({ Title = "Setting", Icon = "settings" }),
	Macro = Window:AddTab({ Title = "Macro", Icon = "cloud-moon" }),
}

local aza = "Ladius HUB Configs"
local bza = tostring(game.PlaceId).."-"..tostring(game.Players.LocalPlayer.Name)

if isfolder(aza) then
	print("have file")
else
	makefolder(aza)
end

function saveSettings()
	local cza = game:GetService("HttpService")
	local dza = cza:JSONEncode(_G)
	if writefile then
		if isfolder(aza) then
			writefile(aza .. "/" .. bza, dza)
		end
	end
end

function loadSettings()
	local cza = game:GetService("HttpService")
	if isfile(aza .. "/" .. bza) then
		_G = cza:JSONDecode(readfile(aza .. "/" .. bza))
	end
end
loadSettings()


-- main

local Main = Tabs.Setting:AddSection("Main") 

local Select_Stage = Main:AddDropdown("Select Stage", {
	Title = "Select Stage",
	Values = {"Toilet City", "Desert", "Cameraman HQ", "Toilet HQ"},
	Multi = false,
	Default = _G.selectedjoin,
	Callback = function(selected)
		_G.selectedjoin = selected
		print(_G.selectedjoin)
		saveSettings()
	end
})

local toggleJoin = Main:AddToggle("toggleJoin", {Title = "Auto Join", Default = _G.join })
toggleJoin:OnChanged(function(bool)
	_G.join = bool
	saveSettings()
end)


task.spawn(function()
	while task.wait() do
		if _G.join then
			pcall(function()
				print("Ez")
			end)
		end
	end
end)




local Setting = Tabs.Setting:AddSection("Setting") 

local toggleSkip = Setting:AddToggle("toggleSkip", {Title = "Auto Skip", Default = _G.Skip })
toggleSkip:OnChanged(function(bool)
	_G.Skip = bool
	saveSettings()
end)

task.spawn(function()
	while task.wait() do
		if _G.Skip then
			pcall(function()
				game:GetService("ReplicatedStorage"):WaitForChild("Events"):WaitForChild("DoubleSpeed"):FireServer()
			end)
		end
	end
end)
