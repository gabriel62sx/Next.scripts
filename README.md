--// [IMPERADOR] • LOADING SCREEN IMPERIAL (MODIFICADO: AZUL & PRETO) //--
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local Lighting = game:GetService("Lighting")
local CoreGui = game:GetService("CoreGui")

local Blur = Instance.new("BlurEffect")
Blur.Size = 0
Blur.Parent = Lighting
TweenService:Create(Blur, TweenInfo.new(0.6), {Size = 18}):Play()

local LoadGui = Instance.new("ScreenGui")
LoadGui.Name = "FuturoReiLoading"
LoadGui.IgnoreGuiInset = true
LoadGui.Parent = CoreGui

local LoadMain = Instance.new("Frame", LoadGui)
LoadMain.Size = UDim2.fromScale(1,1)
LoadMain.BackgroundColor3 = Color3.fromRGB(8,8,8)
LoadMain.BackgroundTransparency = 0.25 

local Logo = Instance.new("TextLabel", LoadMain)
Logo.Size = UDim2.new(0,420,0,60)
Logo.Position = UDim2.fromScale(0.5,0.42)
Logo.AnchorPoint = Vector2.new(0.5,0.5)
Logo.BackgroundTransparency = 1
Logo.Text = "🥶!MPERADO4🥶"
Logo.Font = Enum.Font.GothamBlack
Logo.TextSize = 42
Logo.TextColor3 = Color3.fromRGB(0, 140, 255) -- >> AZUL
Logo.TextTransparency = 1

local Sub = Instance.new("TextLabel", LoadMain)
Sub.Size = UDim2.new(0,420,0,26)
Sub.Position = UDim2.fromScale(0.5,0.48)
Sub.AnchorPoint = Vector2.new(0.5,0.5)
Sub.BackgroundTransparency = 1
Sub.Text = "REI ESTÁ DE VOLTA"
Sub.Font = Enum.Font.GothamMedium
Sub.TextSize = 15
Sub.TextColor3 = Color3.fromRGB(200,200,200)
Sub.TextTransparency = 1

local Phrase = Instance.new("TextLabel", LoadMain)
Phrase.Size = UDim2.new(0,420,0,22)
Phrase.Position = UDim2.fromScale(0.5,0.56)
Phrase.AnchorPoint = Vector2.new(0.5,0.5)
Phrase.BackgroundTransparency = 1
Phrase.Text = ""
Phrase.Font = Enum.Font.GothamSemibold
Phrase.TextSize = 14
Phrase.TextColor3 = Color3.fromRGB(220,220,220)
Phrase.TextTransparency = 1

local BarBg = Instance.new("Frame", LoadMain)
BarBg.Size = UDim2.new(0,380,0,6)
BarBg.Position = UDim2.fromScale(0.5,0.62)
BarBg.AnchorPoint = Vector2.new(0.5,0.5)
BarBg.BackgroundColor3 = Color3.fromRGB(30,30,30)

local Bar = Instance.new("Frame", BarBg)
Bar.Size = UDim2.new(0,0,1,0)
Bar.BackgroundColor3 = Color3.fromRGB(0, 140, 255) -- >> AZUL

Instance.new("UICorner", BarBg).CornerRadius = UDim.new(1,0)
Instance.new("UICorner", Bar).CornerRadius = UDim.new(1,0)

TweenService:Create(Logo, TweenInfo.new(0.6), {TextTransparency = 0}):Play()
TweenService:Create(Sub, TweenInfo.new(0.6), {TextTransparency = 0}):Play()

local phrases = {"ABRINDO CAMINHO PRO REI", "O NOSSO REI VOLTOU", "O REI CHEGOU"}
task.spawn(function()
    for i, text in ipairs(phrases) do
        Phrase.TextTransparency = 1
        Phrase.Text = text
        TweenService:Create(Phrase, TweenInfo.new(0.4), {TextTransparency = 0}):Play()
        task.wait(1.3)
    end
end)

TweenService:Create(Bar, TweenInfo.new(3.8, Enum.EasingStyle.Quad), {Size = UDim2.new(1,0,1,0)}):Play()

task.wait(4.2)

TweenService:Create(LoadMain, TweenInfo.new(0.5), {BackgroundTransparency = 1}):Play()
TweenService:Create(Logo, TweenInfo.new(0.4), {TextTransparency = 1}):Play()
TweenService:Create(Sub, TweenInfo.new(0.4), {TextTransparency = 1}):Play()
TweenService:Create(Phrase, TweenInfo.new(0.4), {TextTransparency = 1}):Play()
TweenService:Create(Blur, TweenInfo.new(0.5), {Size = 0}):Play()

task.delay(0.6, function()
    LoadGui:Destroy()
    Blur:Destroy()
end)

--// INÍCIO DO SCRIPT PRINCIPAL //--

local CoreGui = game:GetService("CoreGui")
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Lighting = game:GetService("Lighting")
local TeleportService = game:GetService("TeleportService")
local HttpService = game:GetService("HttpService")
local StarterGui = game:GetService("StarterGui")
local VirtualUser = game:GetService("VirtualUser")

local LP = Players.LocalPlayer
local Mouse = LP:GetMouse()
local Camera = workspace.CurrentCamera

if CoreGui:FindFirstChild("FuturoReiSupremo") then CoreGui.FuturoReiSupremo:Destroy() end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "FuturoReiSupremo"
ScreenGui.Parent = CoreGui
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

local CrownIconID = "rbxassetid://14567278958" 

-- // PALETA DE CORES: MUDADO PARA AZUL // --
local Colors = {
    Bg = Color3.fromRGB(8, 8, 8),
    DarkBg = Color3.fromRGB(15, 15, 15),
    Accent = Color3.fromRGB(0, 140, 255), -- AZUL VIBRANTE
    White = Color3.fromRGB(255, 255, 255),
    Text = Color3.fromRGB(240, 240, 240),
    Gray = Color3.fromRGB(80, 80, 80)
}

local function MakeDraggable(obj, dragObj)
    local dragging, dragStart, startPos
    dragObj.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            dragStart = input.Position
            startPos = obj.Position
        end
    end)
    dragObj.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end
    end)
    UserInputService.InputChanged:Connect(function(input)
        if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
            local delta = input.Position - dragStart
            TweenService:Create(obj, TweenInfo.new(0.05), {
                Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
            }):Play()
        end
    end)
end

local function CreateCorner(parent, rad)
    local c = Instance.new("UICorner", parent)
    c.CornerRadius = UDim.new(0, rad)
    return c
end

local function Notify(title, msg)
    pcall(function()
        StarterGui:SetCore("SendNotification", {
            Title = title;
            Text = msg;
            Icon = CrownIconID; 
            Duration = 3;
        })
    end)
end

local MiniButton = Instance.new("TextButton")
MiniButton.Name = "MiniButton"
MiniButton.Size = UDim2.new(0, 60, 0, 60)
MiniButton.Position = UDim2.new(0.02, 0, 0.5, 0)
MiniButton.BackgroundColor3 = Colors.Bg
MiniButton.Text = ""
MiniButton.Parent = ScreenGui
CreateCorner(MiniButton, 30)
MakeDraggable(MiniButton, MiniButton)

local MiniStroke = Instance.new("UIStroke", MiniButton)
MiniStroke.Color = Colors.Accent
MiniStroke.Thickness = 3
MiniStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

spawn(function()
    while MiniButton.Parent do
        TweenService:Create(MiniStroke, TweenInfo.new(0.8), {Color = Colors.Accent}):Play()
        wait(0.8)
        TweenService:Create(MiniStroke, TweenInfo.new(0.8), {Color = Colors.Bg}):Play()
        wait(0.8)
    end
end)

local MiniIcon = Instance.new("ImageLabel", MiniButton)
MiniIcon.Size = UDim2.new(0, 35, 0, 35)
MiniIcon.Position = UDim2.new(0.5, -17.5, 0.5, -17.5)
MiniIcon.BackgroundTransparency = 1
MiniIcon.Image = CrownIconID
MiniIcon.ImageColor3 = Colors.White 

local Main = Instance.new("Frame")
Main.Name = "MainFrame"
Main.Size = UDim2.new(0, 720, 0, 480)
Main.Position = UDim2.new(0.5, -360, 0.5, -240)
Main.BackgroundColor3 = Colors.Bg
Main.ClipsDescendants = true
Main.Parent = ScreenGui
Main.Visible = false
CreateCorner(Main, 10)

local MainStroke = Instance.new("UIStroke", Main)
MainStroke.Color = Colors.Accent
MainStroke.Thickness = 2

local Grid = Instance.new("ImageLabel", Main)
Grid.Size = UDim2.new(1, 0, 1, 0)
Grid.Image = "rbxassetid://300138338"
Grid.ImageColor3 = Colors.White
Grid.ImageTransparency = 0.97
Grid.TileSize = UDim2.new(0, 30, 0, 30)
Grid.BackgroundTransparency = 1

local isOpen = false
MiniButton.MouseButton1Click:Connect(function()
    isOpen = not isOpen
    if isOpen then
        Main.Visible = true
        Main.Size = UDim2.new(0, 0, 0, 0)
        TweenService:Create(Main, TweenInfo.new(0.5, Enum.EasingStyle.Back), {Size = UDim2.new(0, 720, 0, 480), BackgroundTransparency = 0}):Play()
    else
        local closeTween = TweenService:Create(Main, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {Size = UDim2.new(0, 0, 0, 0), BackgroundTransparency = 1})
        closeTween:Play()
        closeTween.Completed:Connect(function() Main.Visible = false end)
    end
end)

local Header = Instance.new("Frame", Main)
Header.Size = UDim2.new(1, 0, 0, 55)
Header.BackgroundColor3 = Colors.DarkBg
CreateCorner(Header, 10)
MakeDraggable(Main, Header)

local Title = Instance.new("TextLabel", Header)
Title.Text = "O REI ESTÁ DE VOLTA"
Title.TextColor3 = Colors.White
Title.Font = Enum.Font.GothamBlack
Title.TextSize = 24
Title.Size = UDim2.new(0, 400, 1, 0)
Title.Position = UDim2.new(0, 20, 0, 0)
Title.BackgroundTransparency = 1
Title.TextXAlignment = Enum.TextXAlignment.Left

spawn(function()
    while Title.Parent do
        Title.TextColor3 = Colors.White
        wait(0.5)
        Title.TextColor3 = Colors.Accent -- PISCA AZUL
        wait(0.5)
    end
end)

local Sidebar = Instance.new("Frame", Main)
Sidebar.Size = UDim2.new(0, 180, 1, -55)
Sidebar.Position = UDim2.new(0, 0, 0, 55)
Sidebar.BackgroundColor3 = Colors.DarkBg

local PageContainer = Instance.new("Frame", Main)
PageContainer.Size = UDim2.new(1, -190, 1, -65)
PageContainer.Position = UDim2.new(0, 190, 0, 60)
PageContainer.BackgroundTransparency = 1

local TabsList = Instance.new("UIListLayout", Sidebar)
TabsList.Padding = UDim.new(0, 5)
TabsList.HorizontalAlignment = Enum.HorizontalAlignment.Center

local function AddTab(name, icon)
    local Btn = Instance.new("TextButton", Sidebar)
    Btn.Size = UDim2.new(0.9, 0, 0, 38)
    Btn.BackgroundColor3 = Colors.Bg
    Btn.Text = (icon or "") .. "   " .. name
    Btn.TextColor3 = Colors.Gray
    Btn.Font = Enum.Font.GothamBold
    Btn.TextSize = 13
    Btn.TextXAlignment = Enum.TextXAlignment.Left
    CreateCorner(Btn, 6)
    local pad = Instance.new("UIPadding", Btn)
    pad.PaddingLeft = UDim.new(0, 12)

    local Page = Instance.new("ScrollingFrame", PageContainer)
    Page.Size = UDim2.new(1, 0, 1, 0)
    Page.BackgroundTransparency = 1
    Page.ScrollBarThickness = 2
    Page.ScrollBarImageColor3 = Colors.Accent
    Page.Visible = false
    Instance.new("UIListLayout", Page).Padding = UDim.new(0, 8)
    
    Btn.MouseButton1Click:Connect(function()
        for _, obj in pairs(Sidebar:GetChildren()) do if obj:IsA("TextButton") then obj.BackgroundColor3 = Colors.Bg obj.TextColor3 = Colors.Gray end end
        for _, p in pairs(PageContainer:GetChildren()) do p.Visible = false end
        Page.Visible = true
        Btn.BackgroundColor3 = Colors.Accent
        Btn.TextColor3 = Colors.White
    end)
    return Page
end

local function AddButton(page, text, func)
    local B = Instance.new("TextButton", page)
    B.Size = UDim2.new(0.98, 0, 0, 35)
    B.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    B.Text = text
    B.TextColor3 = Colors.White
    B.Font = Enum.Font.GothamSemibold
    B.TextSize = 13
    CreateCorner(B, 5)
    local Stroke = Instance.new("UIStroke", B)
    Stroke.Color = Colors.White
    Stroke.Thickness = 1
    Stroke.Transparency = 0.8
    B.MouseButton1Click:Connect(function() task.spawn(func) end)
    return B
end

local function AddInputRow(page, btnText, placeholder, func)
    local Container = Instance.new("Frame", page)
    Container.Size = UDim2.new(0.98, 0, 0, 35)
    Container.BackgroundTransparency = 1
    
    local Layout = Instance.new("UIListLayout", Container)
    Layout.FillDirection = Enum.FillDirection.Horizontal
    Layout.Padding = UDim.new(0, 5)

    local B = Instance.new("TextButton", Container)
    B.Size = UDim2.new(0.7, -5, 1, 0)
    B.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    B.Text = btnText
    B.TextColor3 = Colors.White
    B.Font = Enum.Font.GothamSemibold
    B.TextSize = 13
    CreateCorner(B, 5)
    Instance.new("UIStroke", B).Color = Colors.White
    B.UIStroke.Transparency = 0.8

    local T = Instance.new("TextBox", Container)
    T.Size = UDim2.new(0.3, 0, 1, 0)
    T.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    T.PlaceholderText = placeholder
    T.Text = ""
    T.TextColor3 = Colors.White
    T.Font = Enum.Font.GothamMedium
    T.TextSize = 13
    CreateCorner(T, 5)
    Instance.new("UIStroke", T).Color = Colors.Accent
    T.UIStroke.Transparency = 0.5

    B.MouseButton1Click:Connect(function() task.spawn(function() func(T.Text) end) end)
end

local function AddLabel(page, text)
    local L = Instance.new("TextLabel", page)
    L.Size = UDim2.new(0.98, 0, 0, 25)
    L.BackgroundTransparency = 1
    L.Text = ":: " .. string.upper(text) .. " ::"
    L.TextColor3 = Colors.Accent
    L.Font = Enum.Font.GothamBlack
    L.TextSize = 11
end

-- ABA ADMIN
local AdminTab = AddTab("LUGAR DO REI", "🌊")
AddLabel(AdminTab, "Bibliotecas Principais")
AddButton(AdminTab, "Infinite Yield (+400 cmds)", function() loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))() end)
AddButton(AdminTab, "CMD-X (Admin Alternativo)", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/CMD-X/CMD-X/master/Source", true))() end)
AddButton(AdminTab, "Nameless Admin (FE)", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/FilteringEnabled/NamelessAdmin/main/Source"))() end)
AddLabel(AdminTab, "Exploração")
AddButton(AdminTab, "Dark Dex V3", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Babyhamsta/RBLX_Scripts/main/Universal/BypassedDarkDexV3.lua"))() end)
AddButton(AdminTab, "Simple Spy V2 (Remotes)", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/78n/SimpleSpy/main/SimpleSpySource.lua"))() end)

-- ABA JOGADOR
local PlayTab = AddTab("Jogador", "🌊")
AddLabel(PlayTab, "Atributos customizáveis")

-- GOD MODE
AddButton(PlayTab, "GOD MODE (Vida Infinita)", function()
    pcall(function()
        if LP.Character and LP.Character:FindFirstChild("Humanoid") then
            local Humanoid = LP.Character.Humanoid
            Humanoid.MaxHealth = math.huge
            Humanoid.Health = math.huge
            if not LP.Character:FindFirstChild("GodField") then
                local ff = Instance.new("ForceField", LP.Character)
                ff.Name = "GodField"
                ff.Visible = true 
            end
            Notify("GOD MODE", "Ativado! Você é imortal.")
            spawn(function()
                while LP.Character and LP.Character:FindFirstChild("Humanoid") do
                    LP.Character.Humanoid.Health = LP.Character.Humanoid.MaxHealth
                    wait(0.5)
                end
            end)
        end
    end)
end)

AddInputRow(PlayTab, "Definir Velocidade", "Num...", function(val) 
    local num = tonumber(val)
    if num and LP.Character and LP.Character:FindFirstChild("Humanoid") then
        LP.Character.Humanoid.WalkSpeed = num
    end
end)

AddInputRow(PlayTab, "Definir Pulo", "Num...", function(val) 
    local num = tonumber(val)
    if num and LP.Character and LP.Character:FindFirstChild("Humanoid") then
        LP.Character.Humanoid.JumpPower = num
    end
end)

AddLabel(PlayTab, "Outros")
AddButton(PlayTab, "Anti-AFK", function() 
    LP.Idled:connect(function() VirtualUser:CaptureController() VirtualUser:ClickButton2(Vector2.new()) end)
    Notify("Anti-AFK", "Ativado.")
end)
AddButton(PlayTab, "Noclip (Atravessar)", function()
    RunService.Stepped:Connect(function() for _,v in pairs(LP.Character:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide = false end end end)
    Notify("Noclip", "Ativado.")
end)
AddButton(PlayTab, "Fly GUI V3", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))() end)

-- ABA TELEPORTES
local TpTab = AddTab("Teleportes", "🌊")
AddLabel(TpTab, "Teleporte Rápido")

AddButton(TpTab, "Click TP (Ctrl + Click)", function()
    local Mouse = LP:GetMouse()
    Mouse.Button1Down:Connect(function()
        if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) and Mouse.Target then
            LP.Character:MoveTo(Mouse.Hit.p)
        end
    end)
    Notify("Teleporte", "Segure CTRL e Clique para teleportar.")
end)

AddInputRow(TpTab, "TP para Player", "Nome...", function(txt)
    if txt == "" then return end
    for _, p in pairs(Players:GetPlayers()) do
        if string.sub(string.lower(p.Name), 1, string.len(txt)) == string.lower(txt) or string.sub(string.lower(p.DisplayName), 1, string.len(txt)) == string.lower(txt) then
            if p.Character and p.Character:FindFirstChild("HumanoidRootPart") and LP.Character then
                LP.Character.HumanoidRootPart.CFrame = p.Character.HumanoidRootPart.CFrame
                Notify("Sucesso", "Teleportado para: " .. p.Name)
                return
            end
        end
    end
    Notify("Erro", "Jogador não encontrado.")
end)


-- ABA COMBATE
local CombatTab = AddTab("Combate", "🌊")
AddLabel(CombatTab, "Vantagem Tática")

_G.AimbotActive = false
AddButton(CombatTab, "AIMBOT (LIGAR/DESLIGAR)", function()
    _G.AimbotActive = not _G.AimbotActive
    if _G.AimbotActive then
        Notify("Combate", "Aimbot Carregado!")
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/Aimbot-V2/main/Resources/Scripts/Main.lua"))()
    else
        if _G.Aimbot and _G.Aimbot.Settings then _G.Aimbot.Settings.Enabled = false end
        Notify("Combate", "Aimbot Desligado.")
    end
end)

_G.HitboxActive = false
AddButton(CombatTab, "Hitbox Gigante + Wallhack (Toggle)", function()
    _G.HitboxActive = not _G.HitboxActive
    if _G.HitboxActive then
        Notify("Combate", "Hitbox & Visão Ativadas!")
        RunService.RenderStepped:Connect(function()
            if not _G.HitboxActive then return end
            for _, v in pairs(Players:GetPlayers()) do
                if v ~= LP and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
                    v.Character.HumanoidRootPart.Size = Vector3.new(15, 15, 15)
                    v.Character.HumanoidRootPart.Transparency = 1
                    if not v.Character:FindFirstChild("ReiHL") then
                        local hl = Instance.new("Highlight", v.Character)
                        hl.Name = "ReiHL"
                        hl.FillColor = Colors.Accent
                        hl.OutlineColor = Colors.White
                        hl.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                    end
                end
            end
        end)
    else
        Notify("Combate", "Desativado.")
        for _, v in pairs(Players:GetPlayers()) do
            if v.Character and v.Character:FindFirstChild("ReiHL") then v.Character.ReiHL:Destroy() end
            if v.Character and v.Character:FindFirstChild("HumanoidRootPart") then v.Character.HumanoidRootPart.Size = Vector3.new(2,2,1) end
        end
    end
end)
AddButton(CombatTab, "TriggerBot (Auto Click)", function() spawn(function() while wait(0.1) do if Mouse.Target and Mouse.Target.Parent:FindFirstChild("Humanoid") then mouse1click() end end end) end)

-- ABA VISUAIS
local VisTab = AddTab("Visuais", "🌊")
AddLabel(VisTab, "Estilo")
AddButton(VisTab, "Unnamed ESP", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/ic3w0lf22/Unnamed-ESP/master/Main.lua"))() end)
AddButton(VisTab, "Fullbright (Luz)", function() Lighting.Brightness = 2 Lighting.ClockTime = 14 Lighting.GlobalShadows = false end)
AddButton(VisTab, "Raio-X", function() for _,v in pairs(workspace:GetDescendants()) do if v:IsA("BasePart") then v.Transparency = 0.5 end end end)

-- ABA JOGOS/HUBS
local HubTab = AddTab("Script", "🌊")
AddButton(HubTab, "VG Hub (Multi-Jogos)", function() loadstring(game:HttpGet('https://raw.githubusercontent.com/1201n0001/V.G-Hub/main/V.G%20Hub'))() end)
AddButton(HubTab, "Owl Hub (FPS)", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/CriShoux/OwlHub/master/OwlHub.txt"))() end)
AddButton(HubTab, "Blox Fruits (Hoho)", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/acsu123/HOHO_H/main/Loading_UI"))() end)
AddButton(HubTab, "Brookhaven (Ice)", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/IceMael7/NewIceHub/main/Brookhaven"))() end)
AddButton(HubTab, "Doors (Black King)", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/KINGHUB01/BlackKing-obf/main/Doors%20Blackking%20And%20Bobo"))() end)

-- ABA MISC
local MiscTab = AddTab("Misc", "🌊")
AddLabel(MiscTab, "Música & Caos")

AddInputRow(MiscTab, "Tocar Música (Som)", "ID do Som...", function(id)
    if id == "" then return end
    local Sound = Instance.new("Sound", workspace)
    Sound.Name = "FuturoReiSound"
    Sound.SoundId = "rbxassetid://" .. id
    Sound.Volume = 5
    Sound.Looped = true
    Sound:Play()
    Notify("Música", "Tocando ID: " .. id)
end)

AddButton(MiscTab, "Parar Música", function()
    for _, s in pairs(workspace:GetChildren()) do
        if s.Name == "FuturoReiSound" then s:Destroy() end
    end
end)

AddInputRow(MiscTab, "Chat Rainbow (RichText)", "Sua msg...", function(msg)
    if msg == "" then return end
    
    local function toHex(color)
        return string.format("#%02X%02X%02X", color.R * 255, color.G * 255, color.B * 255)
    end
    
    local coloredMsg = ""
    local freq = 0.5
    
    for i = 1, #msg do
        local r = math.sin(freq * i + 0) * 127 + 128
        local g = math.sin(freq * i + 2) * 127 + 128
        local b = math.sin(freq * i + 4) * 127 + 128
        local hex = toHex(Color3.fromRGB(r, g, b))
        coloredMsg = coloredMsg .. '<font color="' .. hex .. '">' .. string.sub(msg, i, i) .. '</font>'
    end
    
    local RS = game:GetService("ReplicatedStorage")
    if RS:FindFirstChild("DefaultChatSystemChatEvents") then
        RS.DefaultChatSystemChatEvents.SayMessageRequest:FireServer(coloredMsg, "All")
        Notify("Chat Rainbow", "Enviado!")
    else
        Notify("Erro", "Chat incompatível com script.")
    end
end)

AddButton(MiscTab, "Fling Universal (Derrubar)", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/0Ben1/fe/main/obf_rf6iQURzs1syxgblQD9UJU8tJAmcC017Cn373866XC747y26hOOi86F87C55532c.lua.txt"))() end)

AddButton(MiscTab, "Spinbot (Girar Rápido)", function()
    local s = Instance.new("BodyAngularVelocity", LP.Character.HumanoidRootPart)
    s.Name = "SpinBot"
    s.AngularVelocity = Vector3.new(0, 100, 0)
    s.MaxTorque = Vector3.new(0, math.huge, 0)
end)

AddButton(MiscTab, "Parar Spinbot", function()
    if LP.Character and LP.Character.HumanoidRootPart:FindFirstChild("SpinBot") then
        LP.Character.HumanoidRootPart.SpinBot:Destroy()
    end
end)

AddButton(MiscTab, "Ficar Invisível", function()
    if LP.Character then LP.Character.HumanoidRootPart.CFrame = CFrame.new(0,9e5,0) wait(0.2) LP.Character.HumanoidRootPart.Anchored = true end
    Notify("Troll", "Invisível.")
end)

-- ABA SERVIDOR
local ServTab = AddTab("Servidor", "🌊")
AddButton(ServTab, "Trocar de Server (Hop)", function() 
    local x={} for _,v in ipairs(HttpService:JSONDecode(game:HttpGetAsync("https://games.roblox.com/v1/games/"..game.PlaceId.."/servers/Public?sortOrder=Asc&limit=100")).data) do if type(v)=="table" and v.maxPlayers>v.playing and v.id~=game.JobId then x[#x+1]=v.id end end
    if #x>0 then TeleportService:TeleportToPlaceInstance(game.PlaceId, x[math.random(1,#x)], LP) end
end)
AddButton(ServTab, "Reentrar", function() TeleportService:Teleport(game.PlaceId, LP) end)

-- // NOVA ABA: TAGS (POSICIONADA APÓS SERVIDOR) // --
local TagTab = AddTab("Tags", "🌊")
AddLabel(TagTab, "Personalização de Rank")

AddButton(TagTab, "ATIVAR TAG SUPREMA (Rainbow)", function()
    pcall(function()
        if LP.Character and LP.Character:FindFirstChild("Head") then
            -- Remove tag antiga se houver
            if LP.Character.Head:FindFirstChild("ReiTag") then LP.Character.Head.ReiTag:Destroy() end
            
            local bg = Instance.new("BillboardGui", LP.Character.Head)
            bg.Name = "ReiTag"
            bg.Size = UDim2.new(0, 300, 0, 60)
            bg.StudsOffset = Vector3.new(0, 3.5, 0)
            bg.AlwaysOnTop = true
            
            local t = Instance.new("TextLabel", bg)
            t.Size = UDim2.new(1,0,1,0)
            t.BackgroundTransparency = 1
            t.TextSize = 22
            t.Font = Enum.Font.GothamBlack
            t.Text = "👑 IMPERADOR SUPREMO 👑"
            t.TextStrokeTransparency = 0
            t.TextStrokeColor3 = Color3.new(0,0,0)
            
            -- Loop Rainbow (Mantido como pedido, mas o script geral está azul)
            task.spawn(function()
                local h = 0
                while bg.Parent do
                    h = (h + 0.01) % 1
                    t.TextColor3 = Color3.fromHSV(h, 1, 1)
                    task.wait(0.04)
                end
            end)
            Notify("Visual", "Tag Imperial Ativada!")
        end
    end)
end)

AddButton(TagTab, "Remover Tag", function()
     if LP.Character and LP.Character:FindFirstChild("Head") and LP.Character.Head:FindFirstChild("ReiTag") then
        LP.Character.Head.ReiTag:Destroy()
        Notify("Tags", "Tag removida.")
     end
end)

--// FINALIZAÇÃO //--
Notify("FUTURO REI", "Imperador Supremo Totalmente Carregado (Azul).")
