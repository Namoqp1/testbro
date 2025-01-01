if not game:IsLoaded() then game.Loaded:Wait() end

repeat task.wait() until game:GetService("Players")
repeat task.wait() until game:GetService("Players").LocalPlayer
repeat task.wait() until game:GetService("ReplicatedStorage")
repeat task.wait() until game:GetService("ReplicatedFirst")

print("up4")


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
local bza = tostring(game.PlaceId)

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
			if game.PlaceId == 118688242561353 then
				pcall(function()
					print(_G.selectedjoin.."kai")
					if _G.selectedjoin == "Toilet City" then
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-233.093933, 233.456894, 820.848511, 1, 3.48396378e-09, 5.44087598e-05, -3.4816896e-09, 1, -4.17993071e-08, -5.44087598e-05, 4.17991188e-08, 1)
					elseif _G.selectedjoin == "Desert" then
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-371.560699, 233.415955, 820.558899, 1, 1.79245496e-09, 1.95014964e-05, -1.79153126e-09, 1, -4.73667079e-08, -1.95014964e-05, 4.73666724e-08, 1)
					elseif _G.selectedjoin == "Cameraman HQ" then
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-113.433075, 233.809219, 822.59137, 0.0469564311, 1.15877548e-07, -0.998896956, -5.13867775e-08, 1, 1.13589905e-07, 0.998896956, 4.59963196e-08, 0.0469564311)
					elseif _G.selectedjoin == "Toilet HQ" then
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-222.731049, 233.456894, 524.083679, -0.07209263, 2.42295783e-08, -0.997397959, -4.1566274e-08, 1, 2.72972294e-08, 0.997397959, 4.3426045e-08, -0.07209263)
					end
				end)
			end
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
			if game.PlaceId ~= 118688242561353 then
				pcall(function()
					game:GetService("ReplicatedStorage"):WaitForChild("Events"):WaitForChild("DoubleSpeed"):FireServer()
				end)
			end
		end
	end
end)


local Macro = Tabs.Macro:AddSection("Macro") 

local Record_Macro = Tabs.Macro:AddSection("Record Macro") 

local RecordMacroTable = {}

local path = "Ladies_Hub/PixelTD/Macro/"

makefolder(path)

local ye = {}

for i,v in pairs(listfiles("Ladies_Hub/PixelTD/Macro/")) do 
	table.insert(ye,({v:gsub("Ladies_Hub/PixelTD/Macro/","")})[1])
end

local nameconfig = nil

local Input = Macro:AddInput("Input", {
	Title = "Create Macro",
	Default = nameconfig,
	Placeholder = "Name Macro",
	Numeric = false,
	Finished = true,
	Callback = function(text)
		nameconfig = text
		writefile(path..nameconfig ..".txt","")
	end
})


local Select_Macro = Macro:AddDropdown("Select Macro", {
	Title = "Select Macro",
	Values = ye,
	Multi = false,
	Default = _G.selectconfig,
	Callback = function(tab)
		_G.selectconfig = tab
		saveSettings()
	end
})

local function Refresh()
	ye = {}
	for i,v in pairs(listfiles("Ladies_Hub/PixelTD/Macro/")) do 
		table.insert(ye,({v:gsub("Ladies_Hub/PixelTD/Macro/","")})[1])
		Select_Macro:SetValues(ye)
	end
end

Macro:AddButton({
	Title = "Refresh Macro",
	Description = "",
	Callback = Refresh
})

Refresh()

Macro:AddButton({
	Title = "Delete file",
	Description = "",
	Callback = function(ez)
	_G.Delete = ez
	delfile(path.._G.selectconfig)
end})


local basetime = 0
spawn(function()
	while true do 
		local realtime_wait = wait()
		if game:GetService("Players").LocalPlayer.PlayerGui.GameGui.Info.Visible == true then 
			basetime = basetime + realtime_wait
		else
			basetime = 0
		end
	end
end)

local xd = nil

local toggleRecord = Record_Macro:AddToggle("toggleRecord", {Title = "Start Record", Default = _G.Skip })
toggleRecord:OnChanged(function(record)
	xd = record
	if xd then 
		RecordMacroTable = {}
	end
end)


local mt = getrawmetatable(game)
local old = mt.__namecall
setreadonly(mt,false)
mt.__namecall = function(self,...)
	if not checkcaller() then 
		local args = {...}
		if xd then
			if self.Name == "ChangeMode" then
				if not args[1]:match("%d") then
					if args[2] then
						table.insert(RecordMacroTable,{
							writefile(path.._G.selectconfig,convert(RecordMacroTable)),
							['time'] = basetime,
							['type'] = "Place",
							['data'] = {
								['name'] = args[1],
								['position'] = args[2]
							}
						})
					end
				elseif args[1]:match("%d") then
					table.insert(RecordMacroTable,{
						writefile(path.._G.selectconfig,convert(RecordMacroTable)),
						['time'] = basetime,
						['type'] = "Upgrade",
						['data'] = {
							['name'] = args[1],
							['position'] = args[2],
							['oldname'] = args[3]:gsub("game%.", "")
						}
					})
				end
			elseif self.Name == "SellTower"  then
				table.insert(RecordMacroTable,{
					writefile(path.._G.selectconfig,convert(RecordMacroTable)),
					['time'] = basetime,
					['type'] = "Sell",
					['data'] = {
						['name'] = args[1]
					}
				})
			end
		end
	end
	return old(self,...)
end





local Play_Macro = Tabs.Macro:AddSection("Play Macro") 


local togglePlay = Play_Macro:AddToggle("togglePlay", {Title = "Play Macro", Default = _G.Play })
togglePlay:OnChanged(function(play)
	_G.Play = play
	saveSettings()
	if _G.Play then 
		local datamacro = readfile(path.._G.selectconfig)
		local real = loadstring("return "..datamacro)()
		for i,v in pairs(real) do 
			if _G.Play then
				repeat wait() until basetime >= v.time
				if v["type"] == "Place" then
					local args = {
						[1] = v.data.name,
						[2] = v.data.position  
					}

					game:GetService("ReplicatedStorage"):WaitForChild("Functions"):WaitForChild("ChangeMode"):InvokeServer(unpack(args))
				elseif v["type"] == "Upgrade" then
					local args = {
						[1] = v.data.name,
						[2] = v.data.position,
						[3] = v.data.oldname,
					}

					game:GetService("ReplicatedStorage"):WaitForChild("Functions"):WaitForChild("ChangeMode"):InvokeServer(unpack(args))
				end
			end
		end
	end
end)

