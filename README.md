local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
	Title = "Ladies_Hub ",
	SubTitle = "Pixel Tower Defend",
	TabWidth = 160,
	Size = UDim2.fromOffset(580, 460),
	Acrylic = false, -- The blur may be detectable, setting this to false disables blur entirely
	Theme = "Dark",
	MinimizeKey = Enum.KeyCode.LeftControl -- Used when theres no MinimizeKeybind
})

local Tabs = {
	Main = Window:AddTab({ Title = "Main", Icon = "home" }),
	Macro = Window:AddTab({ Title = "Macro", Icon = "cloud-moon" }),
	Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}



local aza = "Ladius HUB Configs"
local bza = tostring(game.PlaceId).."-"..tostring(game.Players.LocalPlayer.Name)
function saveSettings()
	local cza = game:GetService("HttpService")
	local dza = cza:JSONEncode(_G)
	if writefile then
		if isfolder(aza) then
			writefile(aza .. "\\" .. bza, dza)
		else
			makefolder(aza)
			writefile(aza .. "\\" .. bza, dza)
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



local Options = Fluent.Options

do

	Tabs.Main:AddParagraph({

		Title = "Main",

		Content = ""
	})
end

local Select_Difficulty = Tabs.Main:AddDropdown("Select_Difficulty", {
	Title = "Select Difficulty",
	Values = {"Easy", "Medium", "Hard", "Nightmare"},
	Multi = false,
	Default = _G.selectedDifficulty,
	Callback = function(selected)
		_G.selectedDifficulty = selected
		saveSettings()
	end
})

local function vote()
	if _G.selectedDifficulty then
		local args = {
			[1] = _G.selectedDifficulty  -- เอาค่าที่เลือกจาก Dropdown มาใส่ใน args
		}

		game:GetService("ReplicatedStorage").Packages._Index:FindFirstChild("sleitnick_knit@1.7.0").knit.Services.VotingService.RF.Vote:InvokeServer(unpack(args))
		print("Voted for difficulty: " .. _G.selectedDifficulty)
	else
		print("Please select a difficulty before voting!")
	end
end

local toggleJoin = Tabs.Main:AddToggle("toggleJoin", {Title = "Auto Vote", Default = _G.Votes })
toggleJoin:OnChanged(function(bool)
	_G.Votes = bool
	saveSettings()
end)

spawn(function()
	while task.wait() do
		if _G.Votes then
			vote()
		end
	end
end)

local play_again = function()
	local again = game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Frames.Results.Main.Foreground.Buttons:FindFirstChild("PlayAgain")
	local again1 = game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Frames.Results:FindFirstChild("Main")

	-- ตรวจสอบว่า again1 มีอยู่หรือไม่ และให้วาร์ปเมื่อ visible
	if again1 and again1.Visible == true then
		again.Size = UDim2.new(5000, 5000, 5000, 5000)
		wait(1.5)
		local VirtualUser = game:GetService('VirtualUser')
		wait(1.5)
		VirtualUser:CaptureController()
		VirtualUser:ClickButton1(Vector2.new(851, 158), game:GetService("Workspace").Camera.CFrame)
	end
end


local toggleRetry = Tabs.Main:AddToggle("toggleRetry", {Title = "Auto Retry", Default = _G.Retry })
toggleRetry:OnChanged(function(booll)
	_G.Retry = booll
	saveSettings()
end)

spawn(function()
	while true do
		wait(1) -- รอ 1 วินาทีระหว่างการตรวจสอบ
		if _G.Retry then
			local again1 = game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Frames.Results:FindFirstChild("Main")

			-- ถ้า again1.Visible == false ให้รอต่อไปจนกว่า Visible จะเป็น true
			if again1 and again1.Visible == true then
				play_again() -- เรียกใช้ฟังก์ชันเมื่อ again1.Visible == true
			else
				-- รอจนกว่า again1.Visible จะเป็น true
				repeat
					wait(1)
					again1 = game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Frames.Results:FindFirstChild("Main")
				until again1 and again1.Visible == true -- ออกจาก loop เมื่อ visible เป็น true

				-- เรียกใช้ play_again() เมื่อเงื่อนไขเป็นจริง
				play_again()
			end
		end
	end
end)


local togglex2 = Tabs.Main:AddToggle("togglex2", {Title = "Auto x2 Speed", Default = _G.speed })
togglex2:OnChanged(function(x2)
	_G.speed = x2
	saveSettings()
end)

spawn(function()
	while task.wait() do
	if _G.speed then
	local Finde = game:GetService("Players").LocalPlayer.PlayerGui.MainUI.SpeedVote:FindFirstChild("Value")
	if Finde.Text == "(0/1)" then
		game:GetService("ReplicatedStorage").Packages._Index:FindFirstChild("sleitnick_knit@1.7.0").knit.Services.WaveService.RF.SpeedUp:InvokeServer()
		end
		end
	end
end)

local toggleskip = Tabs.Main:AddToggle("toggleskip", {Title = "Auto Skip", Default = _G.skip })
toggleskip:OnChanged(function(skip)
	_G.skip = skip
	saveSettings()
end)

spawn(function()
	while task.wait() do
		if _G.skip then
			local bbc = game:GetService("Players").LocalPlayer.PlayerGui.MainUI.GameInfo.AutoSkip:FindFirstChild("TextLabel")
			if bbc.Text == "Auto Skip (0/1)" then
				game:GetService("ReplicatedStorage").Packages._Index:FindFirstChild("sleitnick_knit@1.7.0").knit.Services.WaveService.RF.AutoSkip:InvokeServer()
			end
		end
	end
end)



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



local Options = Fluent.Options

do

	Tabs.Macro:AddParagraph({

		Title = "Macro",

		Content = ""
	})
end

local RecordMacroTable = {}

local path = "Ladies_Hub/PixelTD/Macro/"
makefolder(path)
local ye = {}
for i,v in pairs(listfiles("Ladies_Hub/PixelTD/Macro/")) do 
	table.insert(ye,({v:gsub("Ladies_Hub/PixelTD/Macro/","")})[1])
end

local Input = Tabs.Macro:AddInput("Input", {
	Title = "Create Macro",
	Default = _G.nameconfig,
	Placeholder = "Name Macro",
	Numeric = false, -- Only allows numbers
	Finished = true, -- Only calls callback when you press enter
	Callback = function(text)
		print("Input changed:", text)
		_G.nameconfig = text
		writefile(path.._G.nameconfig ..".txt","")
	end
})

local Select_Macro = Tabs.Macro:AddDropdown(" Select_Macro", {
	Title = "Select Macro",
	Values = ye,
	Multi = false,
	Default = selectconfig,
	Callback = function(tab)
		selectconfig = tab
		print(selectconfig)
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

Tabs.Macro:AddButton({
	Title = "Refresh Macro",
	Description = "",
	Callback = Refresh
})

Refresh()

local basetime = 0
spawn(function()
	while true do 
		local realtime_wait = wait()
		if game:GetService("Players").LocalPlayer.PlayerGui.MainUI.GameInfo.Time.Text ~= "00:00" then 
			basetime = basetime + realtime_wait
		end
	end
end)


-- ตัวแปรเก็บสถานะว่า Toggle เคยเปิดหรือไม่
local wasRecordStarted = false

local toggleRecord = Tabs.Macro:AddToggle("toggleRecord", {Title = "Start Record", Default = startrecord })
toggleRecord:OnChanged(function(boom)
	startrecord = boom

	-- ถ้า Toggle ถูกเปิด
	if startrecord then
		RecordMacroTable = {}  
		wasRecordStarted = true  -- เก็บสถานะว่าถูกเปิดแล้ว
		print("Recording started")
	else
		-- เช็คว่า Toggle เคยถูกเปิดมาก่อนแล้วเพิ่งถูกปิด
		if wasRecordStarted then
			writefile(path..selectconfig, convert(RecordMacroTable))
			print("Recording stopped")
			wasRecordStarted = false  -- รีเซ็ตสถานะว่า Toggle เคยถูกเปิด
		end
	end
end)


local remote_record = {
	"PlaceUnit",
	"UpgradeUnit",
	"SellUnit"
}
local mt = getrawmetatable(game)
local old = mt.__namecall
setreadonly(mt,false)
mt.__namecall = function(self,...)
	if not checkcaller() then 
		local args = {...}
		local deley = -0.6
		if startrecord then
			if self.Name == "PlaceUnit" then

				table.insert(RecordMacroTable,{
					['time'] = basetime+deley,
					['type'] = self.Name,
					['data'] = {
						['name'] = args[1],
						['position'] = args[2]
					}
				})

			elseif table.find(remote_record,self.Name) then 
				table.insert(RecordMacroTable,{
					['time'] = basetime+deley,
					['type'] = self.Name,
					['data'] = {
						['position'] = args[1].HumanoidRootPart.CFrame
					}
				})
			elseif self.Name == "SpeedUp" then
				table.insert(RecordMacroTable,{
					['time'] = basetime+deley,
					['type'] = self.Name
				}
				)

			elseif self.Name == "AutoSkip" then
				table.insert(RecordMacroTable,{
					['time'] = basetime+deley,
					['type'] = self.Name
				}
				)
			end
		end
	end
	return old(self,...)
end







local Options = Fluent.Options

do
	local check = false
	
	if _G.playmacro then
		 abc = "Playing"
		check = true
	else
		if check then
		 abc = "Stoped"
		 check = false
	end
	end


	Tabs.Macro:AddParagraph({

		Title = "Status",

		Content = abc
	})
end




local togglePlay = Tabs.Macro:AddToggle("togglePlay", {Title = "Start Play", Default = _G.playmacro })
togglePlay:OnChanged(function(boo)
	_G.playmacro = boo
	saveSettings()
	if _G.playmacro then 
		local datamacro = readfile(path..selectconfig)

		local real = loadstring("return "..datamacro)()

		for i,v in pairs(real) do 
			if _G.playmacro then 
				repeat wait() until basetime >= v.time

				if v["type"] == "PlaceUnit" then 
					local args = {
						[1] = v.data.name,
						[2] = v.data.position
					}

					game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.7.0"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("UnitService"):WaitForChild("RF"):WaitForChild("PlaceUnit"):InvokeServer(unpack(args))
				elseif v["type"] == "UpgradeUnit" then

					local current = 10
					local current_instance = nil

					for i,unit in pairs(workspace:WaitForChild("Game"):WaitForChild("Map"):WaitForChild("PlacedUnits"):GetChildren()) do 
						local dis = (v.data.position.Position-unit.HumanoidRootPart.Position).Magnitude
						if dis < current then
							current = dis
							current_instance = unit
						end
					end
					if current_instance then
						print("Upgrade")
						local args = {
							[1] = current_instance
						}

						game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.7.0"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("UnitService"):WaitForChild("RF"):WaitForChild("UpgradeUnit"):InvokeServer(unpack(args))
					end

				elseif v["type"] == "SellUnit" then
					local current = 10
					local current_instance = nil

					for i,unit in pairs(workspace:WaitForChild("Game"):WaitForChild("Map"):WaitForChild("PlacedUnits"):GetChildren()) do 
						local dis = (v.data.position.Position-unit.HumanoidRootPart.Position).Magnitude
						if dis < current then
							current = dis
							current_instance = unit
						end
					end
					if current_instance then
						local args = {
							[1] = current_instance
						}

						game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.7.0"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("UnitService"):WaitForChild("RF"):WaitForChild("SellUnit"):InvokeServer(unpack(args))
					end
				elseif v["type"] == "SpeedUp" then
					game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.7.0"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("WaveService"):WaitForChild("RF"):WaitForChild("SpeedUp"):InvokeServer()
				elseif v["type"] == "AutoSkip" then   
					game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.7.0"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("WaveService"):WaitForChild("RF"):WaitForChild("AutoSkip"):InvokeServer()
				end
			end
		end
	end
end)

