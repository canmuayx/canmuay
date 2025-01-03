if game.CoreGui:FindFirstChild('ScreenGui') then
    Fluent:Destroy()
end

local Mapname = 'canmuayx JJ_TEST'

_G.Setting_table = {
    Save_Member = true
}
_G.Check_Save_Setting = "CheckSaveSetting"

getgenv()['JsonEncode'] = function(msg)
    return game:GetService("HttpService"):JSONEncode(msg)
end
getgenv()['JsonDecode'] = function(msg)
    return game:GetService("HttpService"):JSONDecode(msg)
end
getgenv()['Check_Setting'] = function(Name)
    if not _G.Dis and not isfolder(Mapname) then
        makefolder(Mapname)
    end
    if not _G.Dis and not isfile(Mapname.."/"..Name..'.json') then
        writefile(Mapname.."/"..Name..'.json',JsonEncode(_G.Setting_table))
    end
end
getgenv()['Get_Setting'] = function(Name)
    if not _G.Dis and isfolder(Mapname) and isfile(Mapname.."/"..Name..'.json') then
        _G.Setting_table = JsonDecode(readfile(Mapname.."/"..Name..'.json'))
        return _G.Setting_table
    elseif not _G.Dis then
        Check_Setting(Name)
    end
end
getgenv()['Update_Setting'] = function(Name)
    if not _G.Dis and isfolder(Mapname) and isfile(Mapname.."/"..Name..'.json') then
        writefile(Mapname.."/"..Name..'.json',JsonEncode(_G.Setting_table))
    elseif not _G.Dis then
        Check_Setting(Name)
    end
end

Check_Setting(_G.Check_Save_Setting)
Get_Setting(_G.Check_Save_Setting)

if _G.Setting_table.Save_Member then
    getgenv()['MyName'] = game.Players.LocalPlayer.Name
elseif _G.Setting_table.Save_All_Member then
    getgenv()['MyName'] = "AllMember"
else
    getgenv()['MyName'] = "None"
    _G.Dis = true
end

Check_Setting(getgenv()['MyName'])
Get_Setting(getgenv()['MyName'])

_G.Setting_table.Key = _G.wl_key
Update_Setting(getgenv()['MyName'])

if _G.Setting_table == nil then
    _G.Setting_table = {}
end

function update(f ,callback)
    if _G.Setting_table[f] == nil then
        _G.Setting_table[f] = callback
    end
end

local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()
local FluentAll = loadstring(game:HttpGet("https://raw.githubusercontent.com/canmuayx/canmuayx/refs/heads/main/Testing.lua"))()
local GameName = game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name

local Window = Fluent:CreateWindow({
    Title = "Canmuayx Hub " .. GameName,
    SubTitle = "by Canmuayx Hub",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = false,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.RightControl
})

local Tabs = {
    General_Tab = Window:AddTab({ Title = "General", Icon = "house" }),
    Miscellaneous_Tab = Window:AddTab({ Title = "Miscellaneous", Icon = "blinds" })
}

Window:SelectTab(1)

local Options = Fluent.Options

do
    Tabs.General_Tab:AddSection("Farm Main")
    Tabs.General_Tab:AddToggle("MyToggle",{
        Title = "Auto Farm Level", 
        Description = "",
        Default = _G.Setting_table.autofarm,
        Callback = function(vu)
            _G.Setting_table.autofarm = vu
            autofarm = vu
            Update_Setting(getgenv()['MyName'])
    end})

    Tabs.General_Tab:AddToggle("MyToggle",{
        Title = "Auto Unlock Level Cap", 
        Description = "",
        Default = _G.Setting_table.levelcap,
        Callback = function(vu)
            _G.Setting_table.levelcap = vu
            levelcap = vu
            Update_Setting(getgenv()['MyName'])
    end})
    Tabs.General_Tab:AddToggle("MyToggle",{
        Title = "Mob Aura", 
        Description = "",
        Default = _G.Setting_table.mobaura,
        Callback = function(vu)
            _G.Setting_table.mobaura = vu
            mobaura = vu
            Update_Setting(getgenv()['MyName'])
    end})
    Tabs.General_Tab:AddSection("Farm Boss")
    local Boss = {"Finger Bearer","Ocean Curse","Soul Curse","Volcano Curse","Sorcerer Killer","Heian Imaginary Demon"}
    local si = Tabs.General_Tab:AddDropdown("Dropdown", {
        Title = "Select Boss",
        Values = Boss,
        Multi = false,
        Default = "N/A",
        Callback = function (vu)
            _G.selectboss = vu
    end})
    local Mode = {"Easy","Medium","Hard","Nightmare"}
    local si = Tabs.General_Tab:AddDropdown("Dropdown", {
        Title = "Select Mode",
        Values = Mode,
        Multi = false,
        Default = "N/A",
        Callback = function (vu)
            _G.selectmode = vu
    end})
    Tabs.General_Tab:AddToggle("MyToggle",{
        Title = "Auto Join", 
        Description = "",
        Default = false,
        Callback = function(vu)
            autojoin = vu
    end})
    Tabs.General_Tab:AddToggle("MyToggle",{
        Title = "Auto Replay [Wait 30s]", 
        Description = "",
        Default = _G.Setting_table.autoreplay,
        Callback = function(vu)
            _G.Setting_table.autoreplay = vu
            autoreplay = vu
            Update_Setting(getgenv()['MyName'])
    end})
    Tabs.General_Tab:AddToggle("MyToggle",{
        Title = "Auto Farm Boss", 
        Description = "risk getting banned if too fast farm",
        Default = _G.Setting_table.autoboss,
        Callback = function(vu)
            _G.Setting_table.autoboss = vu
            autoboss = vu
            Update_Setting(getgenv()['MyName'])
    end})
    Tabs.General_Tab:AddSection("Options")
    Tabs.General_Tab:AddToggle("MyToggle",{
        Title = "Auto Collect Chest", 
        Description = "",
        Default = true,
        Callback = function(vu)
            autochest = vu
    end})
    Tabs.General_Tab:AddToggle("MyToggle",{
        Title = "Flip Card", 
        Description = "",
        Default = true,
        Callback = function(vu)
            autoflip = vu
    end})
end
do
    local innate = {"Curse Queen","Gambler Fever","Volcano","Star Rage","Infinity","Hydrokinesis","Soul Manipulation","Demon Vessel","Judgeman","Heavenly Restriction","Ratio","Cryokinesis","Construction","Cloning Technique","Tool Manipulation","Straw Doll","Blazing Courage","Blood Manipulation","Curse Speech","Boogie Woogie"}
    local si = Tabs.Miscellaneous_Tab:AddDropdown("Dropdown", {
        Title = "Select Innate",
        Values = innate,
        Multi = false,
        Default = "N/A",
        Callback = function (vu)
            _G.selectinnate = vu
        end
    })
    local ss = Tabs.Miscellaneous_Tab:AddDropdown("Dropdown", {
        Title = "Select Slot",
        Values = {"1","2","3","4"},
        Multi = false,
        Default = "N/A",
        Callback = function (vu)
            _G.selectslot = vu
        end
    })

    Tabs.Miscellaneous_Tab:AddToggle("MyToggle",{
        Title = "Auto Spin Innate", 
        Description = "",
        Default = false,
        Callback = function(vu)
            spininnate = vu
    end})
    Tabs.Miscellaneous_Tab:AddButton({
        Title = "Spin",
        Description = "",
        Callback = function()
            game:GetService("ReplicatedStorage").Remotes.Server.Data.InnateSpin:InvokeServer(_G.selectslot)
            game:GetService("StarterGui"):SetCore("SendNotification",{
                Title = "Spin Innate",
                Text = game:GetService("Players").LocalPlayer.ReplicatedData.innates[_G.selectslot].Value,
                Icon = "rbxassetid://1234567890"
            })
    end})
end

task.spawn(function ()
    while task.wait(.2) do
        pcall(function ()
            local Number = math.random(1, 5)
            if Number == 1 then
                Method = CFrame.new(50,60,0)
            elseif Number == 2 then
                Method = CFrame.new(0,60,50)
            elseif Number == 3 then
                Method = CFrame.new(-50,60,0)
            elseif Number == 4 then
                Method = CFrame.new(0,60,-50)
            elseif Number == 5 then
                Method = CFrame.new(0,60,0)
            end
        end)
    end
end) -- farm_method

game:GetService("RunService").Heartbeat:Connect(function ()
    if mobaura then
        for i,v in next, game:GetService("Workspace").Objects.Mobs:GetChildren() do
            if v.Humanoid.Health > 0 and v:FindFirstChild("HumanoidRootPart") and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= tonumber(100) then
                local args = {
                    [1] = 1,
                    [2] = {
                        [1] = v.Humanoid,
                    }
                }
                
                game:GetService("ReplicatedStorage").Remotes.Server.Combat.M1:FireServer(unpack(args))            
            end
        end
    end
end) -- Mob Aura

task.spawn(function ()
    while task.wait() do
        pcall(function ()
            if autofarm then
                if game:GetService("Players").LocalPlayer.PlayerGui.StorylineDialogue.Frame.QuestFrame.Visible == false then
                    mobaura = false
                    local Missionposition = CFrame.new(-510.823456, 4470.24658, -15619.3047, -0.913292646, -1.66744503e-08, 0.407303959, 7.89997234e-10, 1, 4.2709992e-08, -0.407303959, 3.93284907e-08, -0.913292646)
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Missionposition
                    if (Missionposition.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 5 then
                        wait(3.5)
                        local args = {
                            [1] = {
                                ["type"] = "Capture",
                                ["set"] = "Shijo Town Set",
                                ["rewards"] = {
                                    ["essence"] = 15,
                                    ["cash"] = 50000,
                                    ["exp"] = 8810000,
                                    ["chestMeter"] = 75
                                },
                                ["rewardsText"] = "Script Made By canmuayx",
                                ["difficulty"] = -math.huge,
                                ["title"] = "ez | quest by. canmuayx (ฺBFยังยากกว่าTT)",
                                ["amount"] = 1,
                                ["location"] = workspace.Objects.Locations.Missions:FindFirstChild("Shijo Town Set"):FindFirstChild("Vast Plain"),
                                ["level"] = 430,
                                ["subtitle"] = "",
                                ["grade"] = "Non Sorcerer"
                            }
                        }
                        
                        game:GetService("ReplicatedStorage").Remotes.Server.Data.TakeQuest:InvokeServer(unpack(args))
                    end
                else
                    local namep = game.Players.LocalPlayer.Name
                    for i,v in pairs(workspace.Objects.MissionItems:GetChildren()) do
                        if v.Name == namep and v:IsA("Part") then
                            mobaura = true
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.CFrame * CFrame.new(0,65,0)
                        end
                    end
                end
            end
        end)
    end
end) -- Auto Farm

task.spawn(function ()
    while task.wait() do
        pcall(function ()
            if levelcap then
                if game:GetService("Players").LocalPlayer.PlayerGui.Main.Frame.BottomMiddle.EXP.LevelCapped.Visible == true then
                    game:GetService("ReplicatedStorage").Remotes.Server.Dialogue.GetResponse:InvokeServer("Clan Head Jujutsu High","Start")
                    game:GetService("ReplicatedStorage").Remotes.Server.Dialogue.GetResponse:InvokeServer("Clan Head Jujutsu High","Promote")
                    game:GetService("ReplicatedStorage").Remotes.Server.Dialogue.DialogueFinished:FireServer("Clan Head Jujutsu High")
                end
            end
        end)
    end
end) -- Unlock Level Cap

task.spawn(function ()
    while task.wait() do
        pcall(function ()
            if spininnate then
                for i,v in pairs(game:GetService("Players").LocalPlayer.ReplicatedData.innates:GetChildren()) do
                    if v:IsA("StringValue") then
                        if v.Name == _G.selectslot then
                            if v.Value ~= _G.selectinnate then
                                game:GetService("ReplicatedStorage").Remotes.Server.Data.InnateSpin:InvokeServer(_G.selectslot)
                            end
                        end
                    end
                end
            end
        end)
    end
end) -- Spininnate

task.spawn(function ()
    while task.wait() do
        pcall(function ()
            if autochest then
                if game:GetService("Workspace").Objects.Drops:FindFirstChild("Chest") then
                    game:GetService("VirtualInputManager"):SendKeyEvent(true,101,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                    game:GetService("VirtualInputManager"):SendKeyEvent(false,101,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                end
            end
        end)
    end
end) -- Auto Chest

task.spawn(function ()
    while task.wait() do
        pcall(function ()
            if autoflip then
                if game.PlaceId == 10450270085 then
                    if game:GetService("Players").LocalPlayer.PlayerGui.Loot.Enabled == true then
                        wait(1)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,92,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,276,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,273,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,13,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,13,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        game:GetService("VirtualInputManager"):SendKeyEvent(false,13,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        wait(.25)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,92,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                    end
                else
                    if game:GetService("Players").LocalPlayer.PlayerGui.Loot.Enabled == true then
                        wait(1)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,92,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,13,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        game:GetService("VirtualInputManager"):SendKeyEvent(false,13,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        wait(.25)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,92,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                    end
                end
            end
        end)
    end
end) -- Auto Flip

task.spawn(function ()
    while task.wait() do
        pcall(function ()
            if autoboss then
                if game:GetService("Workspace").Objects.Spawns.BossSpawn:FindFirstChild("QuestMarker") then
                    mobaura = false
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Objects.Spawns.BossSpawn.CFrame
                else
                    for i,v in pairs(game:GetService("Workspace").Objects.Mobs:GetChildren()) do
                        if v.Humanoid.Health > 0 and v:FindFirstChild("HumanoidRootPart") then
                            mobaura = true
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * Method
                        end
                    end
                end
            end
        end)
    end
end) -- Auto Boss

task.spawn(function ()
    while task.wait() do
        pcall(function ()
            if autoreplay then
                if not game:GetService("Workspace").Objects.Drops:FindFirstChild("Chest") then
                    wait(30)
                    if game:GetService("Players").LocalPlayer.PlayerGui.ReadyScreen.Enabled == true then
                        wait(1)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,92,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,13,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        game:GetService("VirtualInputManager"):SendKeyEvent(false,13,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                        wait(.25)
                        game:GetService("VirtualInputManager"):SendKeyEvent(true,92,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
                    end
                end
            end
        end)
    end
end) -- Auto Replay

task.spawn(function ()
    while task.wait() do
        pcall(function ()
            if autojoin then
                if game.PlaceId == 119359147980471 then
                    if _G.selectboss ~= nil and _G.selectmode ~= nil then
                        local args = {
                            [1] = "Boss",
                            [2] = _G.selectboss,
                            [3] = _G.selectmode
                        }
                        
                        game:GetService("ReplicatedStorage").Remotes.Server.Raids.QuickStart:InvokeServer(unpack(args))
                    end
                elseif game.PlaceId == 10450270085 then
                    game:GetService("TeleportService"):Teleport(119359147980471)
                end
            end
        end)
    end
end) -- Auto Join

repeat task.wait() until game:IsLoaded() game:GetService("Players").LocalPlayer.Idled:connect(function()
    game:GetService("VirtualUser"):ClickButton2(Vector2.new())
    game:GetService("VirtualUser"):Button2Down(Vector2.new(0, 0), workspace.CurrentCamera.CFrame)
    wait(1)
    game:GetService("VirtualUser"):Button2Up(Vector2.new(0, 0), workspace.CurrentCamera.CFrame)
end) -- Anti AFK

-- setclipboard(tostring(game.PlaceId))
