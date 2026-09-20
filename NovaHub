--[[
========================================================
                 NOVA HUB V5.2
              BLACK ANIME PREMIUM
========================================================
FIX V5.2:
• Background transparan (game tetep keliatan)
• Float Button ZIndex tinggi (ga ketutup)
• Background toggle (bisa ON/OFF)
• Fix layar hitam
========================================================
]]

--======================================================
-- SERVICES
--======================================================
local Players = game:GetService("Players")
local TeleportService = game:GetService("TeleportService")
local HttpService = game:GetService("HttpService")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local VirtualInputManager = game:GetService("VirtualInputManager")
local UserInputService = game:GetService("UserInputService")
local StarterGui = game:GetService("StarterGui")
local Stats = game:GetService("Stats")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Lighting = game:GetService("Lighting")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")
local Camera = workspace.CurrentCamera

--======================================================
-- CHARACTER
--======================================================
local Character
local Humanoid
local Root

local function UpdateCharacter()
    Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
    Humanoid = Character:WaitForChild("Humanoid")
    Root = Character:WaitForChild("HumanoidRootPart")
end
UpdateCharacter()

LocalPlayer.CharacterAdded:Connect(function()
    task.wait(0.5)
    UpdateCharacter()
end)

--======================================================
-- SECURITY AUTO-ON
--======================================================
pcall(function()
    local oldNamecall
    oldNamecall = hookmetamethod(game, "__namecall", function(self, ...)
        if getnamecallmethod() == "Kick" then return nil end
        return oldNamecall(self, ...)
    end)
end)

LocalPlayer.Idled:Connect(function()
    VirtualInputManager:SendKeyEvent(true, "W", false, game)
    task.wait(0.1)
    VirtualInputManager:SendKeyEvent(false, "W", false, game)
end)

--======================================================
-- THEME
--======================================================
local Theme = {
    Background = Color3.fromRGB(5, 5, 9),
    Secondary = Color3.fromRGB(10, 10, 17),
    Panel = Color3.fromRGB(15, 15, 25),
    Button = Color3.fromRGB(21, 21, 33),
    ButtonHover = Color3.fromRGB(34, 34, 52),
    Accent = Color3.fromRGB(255, 40, 145),
    Purple = Color3.fromRGB(145, 55, 255),
    Blue = Color3.fromRGB(40, 160, 255),
    Green = Color3.fromRGB(40, 230, 140),
    Red = Color3.fromRGB(235, 55, 75),
    White = Color3.fromRGB(245, 245, 255),
    Gray = Color3.fromRGB(150, 150, 170)
}

--======================================================
-- REMOVE OLD GUI
--======================================================
local OldGUI = PlayerGui:FindFirstChild("NovaHubV52")
if OldGUI then OldGUI:Destroy() end

local OldGUI2 = PlayerGui:FindFirstChild("NovaHubV51")
if OldGUI2 then OldGUI2:Destroy() end

--======================================================
-- SCREEN GUI
--======================================================
local GUI = Instance.new("ScreenGui")
GUI.Name = "NovaHubV52"
GUI.ResetOnSpawn = false
GUI.IgnoreGuiInset = true
GUI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
GUI.Parent = PlayerGui

--======================================================
-- BACKGROUND (TRANSPARAN - GAME TETEP KELIATAN)
--======================================================
local Background = Instance.new("Frame")
Background.Size = UDim2.fromScale(1, 1)
Background.BackgroundColor3 = Theme.Background
Background.BackgroundTransparency = 0.5
Background.BorderSizePixel = 0
Background.Visible = true
Background.ZIndex = 0
Background.Parent = GUI

local BackgroundGradient = Instance.new("UIGradient")
BackgroundGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(4, 4, 10)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(18, 5, 27)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(4, 4, 10))
})
BackgroundGradient.Rotation = 45
BackgroundGradient.Transparency = NumberSequence.new({
    NumberSequenceKeypoint.new(0, 0.5),
    NumberSequenceKeypoint.new(0.5, 0.3),
    NumberSequenceKeypoint.new(1, 0.5)
})
BackgroundGradient.Parent = Background

for i = 1, 8 do
    local Orb = Instance.new("Frame")
    local size = math.random(70, 150)
    Orb.Size = UDim2.fromOffset(size, size)
    Orb.Position = UDim2.fromScale(math.random(), math.random())
    Orb.BackgroundColor3 = (i % 2 == 0) and Theme.Purple or Theme.Accent
    Orb.BackgroundTransparency = 0.94
    Orb.BorderSizePixel = 0
    Orb.ZIndex = 0
    Orb.Parent = Background

    local Corner = Instance.new("UICorner")
    Corner.CornerRadius = UDim.new(1, 0)
    Corner.Parent = Orb

    task.spawn(function()
        while Orb.Parent do
            local Tween = TweenService:Create(
                Orb,
                TweenInfo.new(math.random(5, 9), Enum.EasingStyle.Sine, Enum.EasingDirection.InOut),
                {Position = UDim2.fromScale(math.random(), math.random())}
            )
            Tween:Play()
            Tween.Completed:Wait()
        end
    end)
end

--======================================================
-- FLOAT BUTTON (ZINDEX TINGGI BIAR GA KETUTUP)
--======================================================
local FloatButton = Instance.new("TextButton")
FloatButton.Size = UDim2.fromOffset(58, 58)
FloatButton.Position = UDim2.new(0, 18, 0.5, -29)
FloatButton.BackgroundColor3 = Theme.Background
FloatButton.Text = "N"
FloatButton.TextColor3 = Theme.Accent
FloatButton.TextSize = 27
FloatButton.Font = Enum.Font.GothamBold
FloatButton.BorderSizePixel = 0
FloatButton.AutoButtonColor = false
FloatButton.Active = true
FloatButton.Draggable = true
FloatButton.ZIndex = 10
FloatButton.Parent = GUI

local FloatCorner = Instance.new("UICorner")
FloatCorner.CornerRadius = UDim.new(1, 0)
FloatCorner.Parent = FloatButton

local FloatStroke = Instance.new("UIStroke")
FloatStroke.Color = Theme.Accent
FloatStroke.Thickness = 2
FloatStroke.Parent = FloatButton

--======================================================
-- MAIN WINDOW
--======================================================
local Main = Instance.new("Frame")
Main.Size = UDim2.fromOffset(660, 490)
Main.Position = UDim2.fromScale(0.5, 0.5)
Main.AnchorPoint = Vector2.new(0.5, 0.5)
Main.BackgroundColor3 = Theme.Background
Main.BorderSizePixel = 0
Main.Visible = false
Main.ZIndex = 5
Main.Parent = GUI

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 15)
MainCorner.Parent = Main

local MainStroke = Instance.new("UIStroke")
MainStroke.Color = Theme.Accent
MainStroke.Thickness = 2
MainStroke.Parent = Main

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -65, 0, 48)
Title.Position = UDim2.fromOffset(18, 0)
Title.BackgroundTransparency = 1
Title.Text = "✦  N O V A   H U B  V5.2"
Title.TextColor3 = Theme.Accent
Title.TextSize = 20
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.ZIndex = 6
Title.Parent = Main

local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.fromOffset(34, 34)
CloseButton.Position = UDim2.new(1, -44, 0, 7)
CloseButton.BackgroundColor3 = Theme.Red
CloseButton.Text = "×"
CloseButton.TextColor3 = Theme.White
CloseButton.TextSize = 22
CloseButton.Font = Enum.Font.GothamBold
CloseButton.BorderSizePixel = 0
CloseButton.ZIndex = 6
CloseButton.Parent = Main

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(0, 8)
CloseCorner.Parent = CloseButton

-- SIDEBAR
local Sidebar = Instance.new("Frame")
Sidebar.Size = UDim2.new(0, 135, 1, -62)
Sidebar.Position = UDim2.fromOffset(10, 52)
Sidebar.BackgroundColor3 = Theme.Secondary
Sidebar.BorderSizePixel = 0
Sidebar.ZIndex = 6
Sidebar.Parent = Main

local SidebarCorner = Instance.new("UICorner")
SidebarCorner.CornerRadius = UDim.new(0, 10)
SidebarCorner.Parent = Sidebar

local SidebarPadding = Instance.new("UIPadding")
SidebarPadding.PaddingTop = UDim.new(0, 8)
SidebarPadding.PaddingLeft = UDim.new(0, 7)
SidebarPadding.PaddingRight = UDim.new(0, 7)
SidebarPadding.Parent = Sidebar

local SidebarLayout = Instance.new("UIListLayout")
SidebarLayout.Padding = UDim.new(0, 5)
SidebarLayout.SortOrder = Enum.SortOrder.LayoutOrder
SidebarLayout.Parent = Sidebar

-- CONTENT
local Content = Instance.new("Frame")
Content.Size = UDim2.new(1, -155, 1, -62)
Content.Position = UDim2.fromOffset(145, 52)
Content.BackgroundColor3 = Theme.Secondary
Content.BorderSizePixel = 0
Content.ZIndex = 6
Content.Parent = Main

local ContentCorner = Instance.new("UICorner")
ContentCorner.CornerRadius = UDim.new(0, 10)
ContentCorner.Parent = Content

--======================================================
-- PAGE SYSTEM
--======================================================
local Pages = {}

local function CreatePage(Name)
    local Page = Instance.new("ScrollingFrame")
    Page.Name = Name
    Page.Size = UDim2.new(1, -20, 1, -20)
    Page.Position = UDim2.fromOffset(10, 10)
    Page.BackgroundTransparency = 1
    Page.BorderSizePixel = 0
    Page.ScrollBarThickness = 4
    Page.ScrollBarImageColor3 = Theme.Accent
    Page.CanvasSize = UDim2.new(0, 0, 0, 0)
    Page.Visible = false
    Page.ZIndex = 7
    Page.Parent = Content

    local Layout = Instance.new("UIListLayout")
    Layout.Padding = UDim.new(0, 7)
    Layout.SortOrder = Enum.SortOrder.LayoutOrder
    Layout.Parent = Page

    Layout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
        Page.CanvasSize = UDim2.fromOffset(0, Layout.AbsoluteContentSize.Y + 15)
    end)

    Pages[Name] = Page
    return Page
end

local function ShowPage(Name)
    for PageName, Page in pairs(Pages) do
        Page.Visible = PageName == Name
    end
end

--======================================================
-- UI HELPERS
--======================================================
local function Label(Parent, Text)
    local L = Instance.new("TextLabel")
    L.Size = UDim2.new(1, 0, 0, 34)
    L.BackgroundColor3 = Theme.Background
    L.Text = Text
    L.TextColor3 = Theme.Accent
    L.TextSize = 14
    L.Font = Enum.Font.GothamBold
    L.BorderSizePixel = 0
    L.ZIndex = 7
    L.Parent = Parent

    local C = Instance.new("UICorner")
    C.CornerRadius = UDim.new(0, 7)
    C.Parent = L
    return L
end

local function Button(Parent, Text, Callback)
    local B = Instance.new("TextButton")
    B.Size = UDim2.new(1, 0, 0, 38)
    B.BackgroundColor3 = Theme.Button
    B.Text = Text
    B.TextColor3 = Theme.White
    B.TextSize = 13
    B.Font = Enum.Font.GothamBold
    B.BorderSizePixel = 0
    B.AutoButtonColor = false
    B.ZIndex = 7
    B.Parent = Parent

    local C = Instance.new("UICorner")
    C.CornerRadius = UDim.new(0, 7)
    C.Parent = B

    B.MouseEnter:Connect(function() B.BackgroundColor3 = Theme.ButtonHover end)
    B.MouseLeave:Connect(function() B.BackgroundColor3 = Theme.Button end)

    B.Activated:Connect(function()
        local Success, ErrorMessage = pcall(Callback)
        if not Success then warn("[NOVA HUB] " .. tostring(ErrorMessage)) end
    end)

    return B
end

local function Toggle(Parent, Text, Callback)
    local Enabled = false
    local B
    B = Button(Parent, Text .. ": OFF", function()
        Enabled = not Enabled
        B.Text = Text .. ": " .. (Enabled and "ON" or "OFF")
        B.BackgroundColor3 = Enabled and Theme.Green or Theme.Button
        Callback(Enabled)
    end)
    return B
end

local function Slider(Parent, Text, Min, Max, Default, Callback)
    local Frame = Instance.new("Frame")
    Frame.Size = UDim2.new(1, 0, 0, 52)
    Frame.BackgroundColor3 = Theme.Background
    Frame.BorderSizePixel = 0
    Frame.ZIndex = 7
    Frame.Parent = Parent

    local FC = Instance.new("UICorner")
    FC.CornerRadius = UDim.new(0, 7)
    FC.Parent = Frame

    local Title = Instance.new("TextLabel")
    Title.Size = UDim2.new(1, 0, 0, 20)
    Title.BackgroundTransparency = 1
    Title.Text = Text .. ": " .. Default
    Title.TextColor3 = Theme.Accent
    Title.TextSize = 12
    Title.Font = Enum.Font.GothamBold
    Title.TextXAlignment = Enum.TextXAlignment.Left
    Title.ZIndex = 8
    Title.Parent = Frame

    local Pad = Instance.new("UIPadding")
    Pad.PaddingLeft = UDim.new(0, 10)
    Pad.PaddingRight = UDim.new(0, 10)
    Pad.PaddingTop = UDim.new(0, 6)
    Pad.Parent = Frame

    local Bar = Instance.new("Frame")
    Bar.Size = UDim2.new(1, 0, 0, 12)
    Bar.Position = UDim2.new(0, 0, 0, 32)
    Bar.BackgroundColor3 = Theme.Button
    Bar.BorderSizePixel = 0
    Bar.ZIndex = 8
    Bar.Parent = Frame

    local BC = Instance.new("UICorner")
    BC.CornerRadius = UDim.new(1, 0)
    BC.Parent = Bar

    local Fill = Instance.new("Frame")
    Fill.Size = UDim2.new((Default - Min) / (Max - Min), 0, 1, 0)
    Fill.BackgroundColor3 = Theme.Accent
    Fill.BorderSizePixel = 0
    Fill.ZIndex = 9
    Fill.Parent = Bar

    local FillC = Instance.new("UICorner")
    FillC.CornerRadius = UDim.new(1, 0)
    FillC.Parent = Fill

    local dragging = false

    Bar.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
        end
    end)

    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = false
        end
    end)

    UserInputService.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            local rel = (input.Position.X - Bar.AbsolutePosition.X) / Bar.AbsoluteSize.X
            rel = math.clamp(rel, 0, 1)
            Fill.Size = UDim2.new(rel, 0, 1, 0)
            local value = math.floor(Min + (Max - Min) * rel)
            Title.Text = Text .. ": " .. value
            Callback(value)
        end
    end)

    return Frame
end

--======================================================
-- TELEPORT PAGE - SEA 1, 2, 3
--======================================================
local PageTeleport = CreatePage("Teleport")

local Islands = {
    {Name = "Starter Island",   Sea = 1, Pos = Vector3.new(1063, 16, 1450)},
    {Name = "Marine Ford",      Sea = 1, Pos = Vector3.new(-4910, 23, 3990)},
    {Name = "Middle Town",      Sea = 1, Pos = Vector3.new(-658, 7, 1560)},
    {Name = "Jungle",           Sea = 1, Pos = Vector3.new(-1610, 36, 145)},
    {Name = "Pirate Village",   Sea = 1, Pos = Vector3.new(-1180, 5, 3920)},
    {Name = "Desert",           Sea = 1, Pos = Vector3.new(954, 5, 4200)},
    {Name = "Snow Island",      Sea = 1, Pos = Vector3.new(1380, 88, -1300)},
    {Name = "Marine Base",      Sea = 1, Pos = Vector3.new(-2440, 15, -3280)},
    {Name = "Sky Island",       Sea = 1, Pos = Vector3.new(-4900, 720, -2600)},
    {Name = "Prison",           Sea = 1, Pos = Vector3.new(5300, 5, 480)},
    {Name = "Colosseum",        Sea = 1, Pos = Vector3.new(-1500, 5, -3000)},
    {Name = "Magma Village",    Sea = 1, Pos = Vector3.new(-5300, 5, 8500)},
    {Name = "Underwater City",  Sea = 1, Pos = Vector3.new(61000, 800, 1700)},
    {Name = "Fountain City",    Sea = 1, Pos = Vector3.new(5250, 65, 4050)},
    {Name = "Frozen Village",   Sea = 1, Pos = Vector3.new(1210, 5, -1320)},
    {Name = "Graveyard",        Sea = 1, Pos = Vector3.new(-5515, 5, -2000)},
    {Name = "Cursed Ship",      Sea = 1, Pos = Vector3.new(930, 125, 32750)},
    {Name = "Ice Castle",       Sea = 1, Pos = Vector3.new(5550, 60, -2800)},
    {Name = "Forgotten Island", Sea = 1, Pos = Vector3.new(-3050, 240, -7500)},
    {Name = "Haunted Castle",   Sea = 1, Pos = Vector3.new(-9500, 140, 6000)},
    {Name = "Hydra Island",     Sea = 1, Pos = Vector3.new(5750, 620, -280)},

    {Name = "Kingdom of Rose",  Sea = 2, Pos = Vector3.new(-393, 80, 3825)},
    {Name = "Green Zone",       Sea = 2, Pos = Vector3.new(-77, 85, 3070)},
    {Name = "Graveyard",        Sea = 2, Pos = Vector3.new(5150, 80, 400)},
    {Name = "Snow Mountain",    Sea = 2, Pos = Vector3.new(1350, 400, -1500)},
    {Name = "Hot and Cold",     Sea = 2, Pos = Vector3.new(-5375, 60, -2560)},
    {Name = "Cursed Ship",      Sea = 2, Pos = Vector3.new(930, 125, 32750)},
    {Name = "Ice Castle",       Sea = 2, Pos = Vector3.new(5550, 60, -2800)},
    {Name = "Forgotten Island", Sea = 2, Pos = Vector3.new(-3050, 240, -7500)},
    {Name = "Haunted Castle",   Sea = 2, Pos = Vector3.new(-9500, 140, 6000)},
    {Name = "Hydra Island",     Sea = 2, Pos = Vector3.new(5750, 620, -280)},
    {Name = "Great Tree",       Sea = 2, Pos = Vector3.new(2000, 500, -3000)},
    {Name = "Castle On The Sea",Sea = 2, Pos = Vector3.new(-5000, 313, -4400)},
    {Name = "Floating Turtle",  Sea = 2, Pos = Vector3.new(-11500, 400, -10800)},

    {Name = "Port Town",        Sea = 3, Pos = Vector3.new(-280, 6, 3000)},
    {Name = "Hydra Island",     Sea = 3, Pos = Vector3.new(5750, 620, -280)},
    {Name = "Great Tree",       Sea = 3, Pos = Vector3.new(2000, 500, -3000)},
    {Name = "Castle On The Sea",Sea = 3, Pos = Vector3.new(-5000, 313, -4400)},
    {Name = "Kitsune Island",   Sea = 3, Pos = Vector3.new(-13000, 300, -4000)},
    {Name = "Tiki Outpost",     Sea = 3, Pos = Vector3.new(-13800, 5, -180)},
    {Name = "Floating Turtle",  Sea = 3, Pos = Vector3.new(-11500, 400, -10800)},
    {Name = "Haunted Castle",   Sea = 3, Pos = Vector3.new(-9500, 140, 6000)},
    {Name = "Sea of Treats",    Sea = 3, Pos = Vector3.new(-1750, 30, -650)},
}

local Teleporting = false

local function TeleportTo(Position)
    if Teleporting then return end
    if not Root or not Root.Parent then UpdateCharacter() end
    if not Root then return end

    Teleporting = true

    pcall(function()
        Root.CFrame = CFrame.new(Position + Vector3.new(0, 3, 0))
    end)

    task.delay(0.4, function()
        Teleporting = false
    end)
end

Label(PageTeleport, "🌊 SEA 1")
for _, Island in ipairs(Islands) do
    if Island.Sea == 1 then
        Button(PageTeleport, "📍 " .. Island.Name, function()
            TeleportTo(Island.Pos)
        end)
    end
end

Label(PageTeleport, "🌊 SEA 2")
for _, Island in ipairs(Islands) do
    if Island.Sea == 2 then
        Button(PageTeleport, "📍 " .. Island.Name .. " (S2)", function()
            TeleportTo(Island.Pos)
        end)
    end
end

Label(PageTeleport, "🌊 SEA 3")
for _, Island in ipairs(Islands) do
    if Island.Sea == 3 then
        Button(PageTeleport, "📍 " .. Island.Name .. " (S3)", function()
            TeleportTo(Island.Pos)
        end)
    end
end

Label(PageTeleport, "🛠️ UTILITY")

Button(PageTeleport, "📋 COPY POSITION", function()
    if Root then
        local pos = Root.Position
        local text = string.format("%.0f, %.0f, %.0f", pos.X, pos.Y, pos.Z)
        pcall(function()
            if setclipboard then setclipboard(text) end
        end)
        pcall(function()
            StarterGui:SetCore("SendNotification", {
                Title = "COPIED",
                Text = text,
                Duration = 3
            })
        end)
    end
end)

Button(PageTeleport, "🖱️ TP TO MOUSE", function()
    if Root then
        local mouse = LocalPlayer:GetMouse()
        if mouse.Hit then
            Root.CFrame = mouse.Hit + Vector3.new(0, 3, 0)
        end
    end
end)

--======================================================
-- MOVEMENT PAGE
--======================================================
local PageMove = CreatePage("Move")
Label(PageMove, "🏃 MOVEMENT")

Slider(PageMove, "WalkSpeed", 16, 500, 16, function(val)
    if Humanoid then Humanoid.WalkSpeed = val end
end)

Slider(PageMove, "JumpPower", 50, 500, 50, function(val)
    if Humanoid then Humanoid.JumpPower = val Humanoid.UseJumpPower = true end
end)

Toggle(PageMove, "INFINITE JUMP", function(state)
    _G.NovaInfJump = state
    if state then
        task.spawn(function()
            while _G.NovaInfJump do
                task.wait()
                if UserInputService:IsKeyDown(Enum.KeyCode.Space) and Humanoid then
                    Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
                end
            end
        end)
    end
end)

Toggle(PageMove, "NOCLIP", function(state)
    _G.NovaNoclip = state
    if state then
        task.spawn(function()
            while _G.NovaNoclip do
                task.wait()
                if Character then
                    for _, part in ipairs(Character:GetDescendants()) do
                        if part:IsA("BasePart") then part.CanCollide = false end
                    end
                end
            end
        end)
    else
        if Character then
            for _, part in ipairs(Character:GetDescendants()) do
                if part:IsA("BasePart") then part.CanCollide = true end
            end
        end
    end
end)

local flyOn = false
local flyBV, flyBG

Toggle(PageMove, "FLY", function(state)
    flyOn = state
    if state and Root then
        flyBV = Instance.new("BodyVelocity")
        flyBV.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
        flyBV.Velocity = Vector3.zero
        flyBV.Parent = Root

        flyBG = Instance.new("BodyGyro")
        flyBG.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
        flyBG.P = 9e4
        flyBG.Parent = Root

        task.spawn(function()
            while flyOn do
                task.wait()
                if not Root then break end
                local move = Vector3.zero
                if UserInputService:IsKeyDown(Enum.KeyCode.W) then move += Camera.CFrame.LookVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.S) then move -= Camera.CFrame.LookVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.A) then move -= Camera.CFrame.RightVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.D) then move += Camera.CFrame.RightVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.Space) then move += Vector3.new(0,1,0) end
                if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then move -= Vector3.new(0,1,0) end
                flyBV.Velocity = move * 100
                flyBG.CFrame = Camera.CFrame
            end
        end)
    else
        if flyBV then flyBV:Destroy() end
        if flyBG then flyBG:Destroy() end
    end
end)

Toggle(PageMove, "FULL BRIGHT", function(state)
    if state then
        Lighting.Ambient = Color3.fromRGB(255,255,255)
        Lighting.Brightness = 2
        Lighting.OutdoorAmbient = Color3.fromRGB(255,255,255)
    else
        Lighting.Ambient = Color3.fromRGB(70,70,70)
        Lighting.Brightness = 1
        Lighting.OutdoorAmbient = Color3.fromRGB(128,128,128)
    end
end)

--======================================================
-- FULL MOON PAGE
--======================================================
local PageMoon = CreatePage("Moon")
Label(PageMoon, "🌕 FULL MOON")

local MoonStatus = Instance.new("TextLabel")
MoonStatus.Size = UDim2.new(1, 0, 0, 65)
MoonStatus.BackgroundColor3 = Theme.Background
MoonStatus.Text = "🌙 CHECKING..."
MoonStatus.TextColor3 = Theme.Gray
MoonStatus.TextSize = 15
MoonStatus.Font = Enum.Font.GothamBold
MoonStatus.BorderSizePixel = 0
MoonStatus.ZIndex = 7
MoonStatus.Parent = PageMoon

local MoonCorner = Instance.new("UICorner")
MoonCorner.CornerRadius = UDim.new(0, 8)
MoonCorner.Parent = MoonStatus

local function IsFullMoon()
    local attr = Lighting:GetAttribute("FullMoon")
    if attr ~= nil then return attr == true end
    local bv = Lighting:FindFirstChild("FullMoon")
    if bv and bv:IsA("BoolValue") then return bv.Value end
    local rv = ReplicatedStorage:FindFirstChild("FullMoon")
    if rv and rv:IsA("BoolValue") then return rv.Value end
    return false
end

local function UpdateMoonStatus()
    if IsFullMoon() then
        MoonStatus.Text = "🌕 FULL MOON ACTIVE"
        MoonStatus.TextColor3 = Theme.Green
    else
        MoonStatus.Text = "🌙 FULL MOON NOT ACTIVE"
        MoonStatus.TextColor3 = Theme.Gray
    end
end

task.spawn(function()
    while GUI.Parent do
        UpdateMoonStatus()
        task.wait(1)
    end
end)

Button(PageMoon, "🔄 REFRESH MOON", UpdateMoonStatus)

--======================================================
-- PLAYER PAGE
--======================================================
local PagePlayers = CreatePage("Players")
Label(PagePlayers, "👥 PLAYER LIST")

local PlayerContainer = Instance.new("Frame")
PlayerContainer.Size = UDim2.new(1, 0, 0, 0)
PlayerContainer.BackgroundTransparency = 1
PlayerContainer.ZIndex = 7
PlayerContainer.Parent = PagePlayers

local PlayerLayout = Instance.new("UIListLayout")
PlayerLayout.Padding = UDim.new(0, 5)
PlayerLayout.Parent = PlayerContainer

local function RefreshPlayers()
    for _, obj in ipairs(PlayerContainer:GetChildren()) do
        if obj:IsA("TextButton") then obj:Destroy() end
    end
    for _, player in ipairs(Players:GetPlayers()) do
        local b = Button(PlayerContainer, "👤 " .. player.DisplayName .. "  @" .. player.Name, function()
            if player.Character then
                local pRoot = player.Character:FindFirstChild("HumanoidRootPart")
                if pRoot then TeleportTo(pRoot.Position) end
            end
        end)
        b.Parent = PlayerContainer
    end
end

Players.PlayerAdded:Connect(RefreshPlayers)
Players.PlayerRemoving:Connect(RefreshPlayers)
RefreshPlayers()

--======================================================
-- PVP PAGE
--======================================================
local PagePVP = CreatePage("PVP")
Label(PagePVP, "🎯 LOCK TARGET")

local lockedPlayer = nil
local lockBtn

local function updateLockBtn()
    if lockedPlayer then
        lockBtn.Text = "LOCKED: " .. lockedPlayer.Name
        lockBtn.BackgroundColor3 = Theme.Green
    else
        lockBtn.Text = "LOCK TARGET: NONE"
        lockBtn.BackgroundColor3 = Theme.Button
    end
end

lockBtn = Button(PagePVP, "LOCK TARGET: NONE", function()
    local list = {}
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LocalPlayer then table.insert(list, p) end
    end
    if #list == 0 then return end
    local idx = 0
    for i, p in ipairs(list) do
        if p == lockedPlayer then idx = i break end
    end
    local ni = idx + 1
    if ni > #list then ni = 1 end
    lockedPlayer = list[ni]
    updateLockBtn()
end)

Button(PagePVP, "UNLOCK TARGET", function()
    lockedPlayer = nil
    updateLockBtn()
end)

Label(PagePVP, "🎯 AIMBOT")

local aimOn = false
local aimFov = 300
local aimOffsetX = 0
local aimOffsetY = -30

local function getTargetHrp()
    if lockedPlayer and lockedPlayer.Character then
        local h = lockedPlayer.Character:FindFirstChild("Humanoid")
        local hrpP = lockedPlayer.Character:FindFirstChild("HumanoidRootPart")
        if h and hrpP and h.Health > 0 then return hrpP end
        return nil
    end
    local closest, dist = nil, aimFov
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LocalPlayer and p.Character then
            local h = p.Character:FindFirstChild("Humanoid")
            local hrpP = p.Character:FindFirstChild("HumanoidRootPart")
            if h and hrpP and h.Health > 0 then
                local pos, vis = Camera:WorldToViewportPoint(hrpP.Position)
                if vis then
                    local d = (Vector2.new(pos.X, pos.Y) - Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)).Magnitude
                    if d < dist then dist = d closest = hrpP end
                end
            end
        end
    end
    return closest
end

Toggle(PagePVP, "AIMBOT", function(state)
    aimOn = state
    if state then
        task.spawn(function()
            while aimOn do
                task.wait()
                local t = getTargetHrp()
                if t then
                    local offset = Vector3.new(aimOffsetX, aimOffsetY, 0)
                    Camera.CFrame = CFrame.new(Camera.CFrame.Position, t.Position + offset)
                end
            end
        end)
    end
end)

Button(PagePVP, "FOV: 300", function()
    if aimFov == 300 then aimFov = 500
    elseif aimFov == 500 then aimFov = 150
    else aimFov = 300 end
end)

Label(PagePVP, "⚡ AUTO SKILL AIM (SILENT)")

local autoSkill = false

local function silentAimFire(targetPos)
    if not targetPos then return end
    local savedCamCF = Camera.CFrame
    local offset = Vector3.new(aimOffsetX, aimOffsetY, 0)
    Camera.CFrame = CFrame.new(Camera.CFrame.Position, targetPos + offset)

    local tool = Character and Character:FindFirstChildOfClass("Tool")
    if tool then
        for _, child in ipairs(tool:GetChildren()) do
            if child:IsA("RemoteEvent") then
                pcall(function() child:FireServer() end)
            elseif child:IsA("RemoteFunction") then
                pcall(function() child:InvokeServer() end)
            end
        end
        pcall(function() tool:Activate() end)
    end

    pcall(function()
        VirtualInputManager:SendKeyEvent(true, "Z", false, game)
        task.wait(0.03)
        VirtualInputManager:SendKeyEvent(false, "Z", false, game)
    end)

    task.wait(0.05)
    Camera.CFrame = savedCamCF
end

Toggle(PagePVP, "AUTO SKILL AIM", function(state)
    autoSkill = state
    if state then
        task.spawn(function()
            while autoSkill do
                task.wait(0.1)
                local t = getTargetHrp()
                if t then silentAimFire(t.Position) end
            end
        end)
    end
end)

--======================================================
-- ESP PAGE
--======================================================
local PageESP = CreatePage("ESP")
Label(PageESP, "👁 PLAYER ESP")

local PlayerESP = false

local function RemovePlayerESP()
    for _, p in ipairs(Players:GetPlayers()) do
        if p.Character then
            for _, obj in ipairs(p.Character:GetDescendants()) do
                if obj.Name == "NovaESP" then obj:Destroy() end
            end
        end
    end
end

local function AddPlayerESP(player)
    if player == LocalPlayer then return end
    local character = player.Character
    if not character then return end
    local root = character:FindFirstChild("HumanoidRootPart")
    if not root or root:FindFirstChild("NovaESP") then return end

    local b = Instance.new("BillboardGui")
    b.Name = "NovaESP"
    b.Size = UDim2.fromOffset(120, 30)
    b.StudsOffset = Vector3.new(0, 3, 0)
    b.AlwaysOnTop = true
    b.Parent = root

    local t = Instance.new("TextLabel")
    t.Size = UDim2.fromScale(1, 1)
    t.BackgroundTransparency = 1
    t.Text = player.DisplayName
    t.TextColor3 = Theme.Accent
    t.TextStrokeTransparency = 0
    t.TextSize = 13
    t.Font = Enum.Font.GothamBold
    t.Parent = b
end

Toggle(PageESP, "PLAYER ESP", function(state)
    PlayerESP = state
    if not state then RemovePlayerESP() end
end)

task.spawn(function()
    while GUI.Parent do
        task.wait(1)
        if PlayerESP then
            for _, p in ipairs(Players:GetPlayers()) do AddPlayerESP(p) end
        end
    end
end)

Label(PageESP, "🍎 FRUIT ESP")

local FruitList = {
    "Rocket","Spin","Chop","Spring","Bomb","Smoke","Spike","Flame",
    "Falcon","Ice","Sand","Dark","Diamond","Light","Rubber","Barrier",
    "Magma","Door","Quake","Buddha","Love","Spider","Sound","Phoenix",
    "Portal","Rumble","Pain","Blizzard","Gravity","Mammoth","T-Rex",
    "Dough","Shadow","Venom","Control","Spirit","Dragon","Leopard",
    "Kitsune","Yeti","Gas"
}

local FruitESP = false
local activeFruitESP = {}

local function getFruitName(name)
    for _, n in ipairs(FruitList) do
        if name == n or name:find("^" .. n .. "[%-%s]") then return n end
    end
    return nil
end

local function ClearFruitESP()
    for obj, gui in pairs(activeFruitESP) do
        if gui and gui.Parent then gui:Destroy() end
    end
    activeFruitESP = {}
end

Toggle(PageESP, "FRUIT ESP", function(state)
    FruitESP = state
    if not state then ClearFruitESP() end
    if state then
        task.spawn(function()
            while FruitESP and GUI.Parent do
                task.wait(0.5)
                for obj, gui in pairs(activeFruitESP) do
                    if not obj or not obj.Parent then
                        if gui and gui.Parent then gui:Destroy() end
                        activeFruitESP[obj] = nil
                    end
                end
                for _, obj in ipairs(workspace:GetDescendants()) do
                    if (obj:IsA("Tool") or obj:IsA("Model")) and not activeFruitESP[obj] and obj:FindFirstChild("Handle") then
                        local fn = getFruitName(obj.Name)
                        if fn then
                            local b = Instance.new("BillboardGui")
                            b.Name = "NovaFruitESP"
                            b.Size = UDim2.fromOffset(90, 30)
                            b.AlwaysOnTop = true
                            b.StudsOffset = Vector3.new(0, 3, 0)
                            b.Parent = obj

                            local t = Instance.new("TextLabel", b)
                            t.Size = UDim2.fromScale(1, 1)
                            t.BackgroundTransparency = 1
                            t.Text = fn
                            t.TextColor3 = Theme.Accent
                            t.TextStrokeTransparency = 0
                            t.TextScaled = true
                            t.Font = Enum.Font.GothamBold

                            activeFruitESP[obj] = b
                        end
                    end
                end
            end
        end)
    end
end)

--======================================================
-- HOP + LUCK PAGE
--======================================================
local PageHop = CreatePage("Hop")
Label(PageHop, "🔄 SERVER HOP")

local hopping = false

local function GetServers()
    local url = "https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/Public?sortOrder=Asc&limit=100"
    local ok, result = pcall(function()
        return HttpService:JSONDecode(game:HttpGet(url))
    end)
    if not ok or not result then return {} end
    return result.data or {}
end

local function ServerHop(force)
    if hopping and not force then return end
    hopping = true
    local servers = GetServers()
    local available = {}
    for _, s in ipairs(servers) do
        if s.id ~= game.JobId and s.playing < s.maxPlayers then
            table.insert(available, s.id)
        end
    end
    if #available > 0 then
        local id = available[math.random(1, #available)]
        TeleportService:TeleportToPlaceInstance(game.PlaceId, id, LocalPlayer)
    end
    task.delay(6, function() hopping = false end)
end

Button(PageHop, "🔄 HOP SERVER", ServerHop)

Label(PageHop, "💎 MYTHICAL SNIPER")

local MythicalList = {
    "Dragon","Leopard","Kitsune","Yeti","Gas",
    "Dough","Shadow","Venom","Control","Spirit"
}

local hopCooldown = 0

local function safeHop()
    if tick() - hopCooldown < 5 then return end
    hopCooldown = tick()
    ServerHop(true)
end

local mythSniperOn = false

Toggle(PageHop, "MYTHICAL SNIPER", function(state)
    mythSniperOn = state
    if state then
        task.spawn(function()
            while mythSniperOn do
                task.wait(0.5)
                local found = false
                for _, obj in ipairs(workspace:GetDescendants()) do
                    if obj:IsA("Tool") or obj:IsA("Model") then
                        if obj:FindFirstChild("Handle") then
                            for _, myth in ipairs(MythicalList) do
                                if obj.Name == myth or obj.Name:find("^" .. myth .. "[%-%s]") then
                                    found = true
                                    pcall(function()
                                        StarterGui:SetCore("SendNotification", {
                                            Title = "MYTHICAL!", Text = myth, Duration = 10
                                        })
                                    end)
                                    if Root then
                                        pcall(function()
                                            Root.CFrame = obj.Handle.CFrame * CFrame.new(0, 3, 0)
                                        end)
                                    end
                                    task.wait(0.5)
                                    pcall(function()
                                        firetouchinterest(Root, obj.Handle, 0)
                                        firetouchinterest(Root, obj.Handle, 1)
                                    end)
                                    mythSniperOn = false
                                    break
                                end
                            end
                        end
                        if found then break end
                    end
                end
                if not found then safeHop() end
            end
        end)
    end
end)

Button(PageHop, "HOP CARI MYTHICAL", safeHop)

--======================================================
-- INFO PAGE
--======================================================
local PageInfo = CreatePage("Info")
Label(PageInfo, "📊 INFO")

local InfoLabel = Instance.new("TextLabel")
InfoLabel.Size = UDim2.new(1, 0, 0, 180)
InfoLabel.BackgroundColor3 = Theme.Background
InfoLabel.TextColor3 = Theme.White
InfoLabel.TextSize = 14
InfoLabel.Font = Enum.Font.Gotham
InfoLabel.TextXAlignment = Enum.TextXAlignment.Left
InfoLabel.TextYAlignment = Enum.TextYAlignment.Top
InfoLabel.BorderSizePixel = 0
InfoLabel.ZIndex = 7
InfoLabel.Parent = PageInfo

local InfoPadding = Instance.new("UIPadding")
InfoPadding.PaddingLeft = UDim.new(0, 12)
InfoPadding.PaddingTop = UDim.new(0, 10)
InfoPadding.Parent = InfoLabel

local FPS = 0
local FrameCount = 0
local FPSTime = 0

RunService.RenderStepped:Connect(function(DeltaTime)
    FrameCount += 1
    FPSTime += DeltaTime
    if FPSTime >= 1 then
        FPS = math.floor(FrameCount / FPSTime)
        FrameCount = 0
        FPSTime = 0
    end
end)

local function GetPing()
    local p = 0
    pcall(function()
        p = Stats.Network.ServerStatsItem["Data Ping"]:GetValue()
    end)
    return math.floor(p)
end

task.spawn(function()
    while GUI.Parent do
        task.wait(0.5)
        local posText = "N/A"
        if Root and Root.Parent then
            local p = Root.Position
            posText = string.format("%.0f, %.0f, %.0f", p.X, p.Y, p.Z)
        end
        InfoLabel.Text =
            "Player: " .. LocalPlayer.Name ..
            "\nUser ID: " .. LocalPlayer.UserId ..
            "\nFPS: " .. FPS ..
            "\nPing: " .. GetPing() .. " ms" ..
            "\nPosition: " .. posText
    end
end)

--======================================================
-- SETTINGS PAGE
--======================================================
local PageSettings = CreatePage("Settings")
Label(PageSettings, "⚙ SETTINGS")

Button(PageSettings, "🔄 RECONNECT", function()
    TeleportService:Teleport(game.PlaceId, LocalPlayer)
end)

Button(PageSettings, "💀 RESET CHARACTER", function()
    if Humanoid then Humanoid.Health = 0 end
end)

local bgEnabled = true

Button(PageSettings, "🌌 BACKGROUND: ON", function()
    bgEnabled = not bgEnabled
    Background.Visible = bgEnabled
end)

local function SetAccent(Color)
    Theme.Accent = Color
    MainStroke.Color = Color
    FloatStroke.Color = Color
    Title.TextColor3 = Color
    FloatButton.TextColor3 = Color
    for _, Page in pairs(Pages) do
        for _, obj in ipairs(Page:GetChildren()) do
            if obj:IsA("TextLabel") and obj.BackgroundColor3 == Theme.Background then
                obj.TextColor3 = Color
            end
        end
    end
end

Button(PageSettings, "🩷 PINK NEON", function() SetAccent(Color3.fromRGB(255, 40, 145)) end)
Button(PageSettings, "💜 PURPLE NEON", function() SetAccent(Color3.fromRGB(160, 60, 255)) end)
Button(PageSettings, "💙 BLUE NEON", function() SetAccent(Color3.fromRGB(40, 160, 255)) end)
Button(PageSettings, "💚 GREEN NEON", function() SetAccent(Color3.fromRGB(40, 230, 140)) end)

--======================================================
-- SIDEBAR
--======================================================
local function CreateSidebarButton(Name, Icon)
    local B = Instance.new("TextButton")
    B.Size = UDim2.new(1, 0, 0, 34)
    B.BackgroundColor3 = Theme.Button
    B.Text = Icon .. " " .. Name
    B.TextColor3 = Theme.White
    B.TextSize = 12
    B.Font = Enum.Font.GothamBold
    B.BorderSizePixel = 0
    B.AutoButtonColor = false
    B.ZIndex = 7
    B.Parent = Sidebar

    local C = Instance.new("UICorner")
    C.CornerRadius = UDim.new(0, 7)
    C.Parent = B

    B.MouseEnter:Connect(function() B.BackgroundColor3 = Theme.ButtonHover end)
    B.MouseLeave:Connect(function() B.BackgroundColor3 = Theme.Button end)
    B.Activated:Connect(function() ShowPage(Name) end)

    return B
end

CreateSidebarButton("Teleport", "⚡")
CreateSidebarButton("Move", "🏃")
CreateSidebarButton("Moon", "🌕")
CreateSidebarButton("Players", "👥")
CreateSidebarButton("PVP", "🎯")
CreateSidebarButton("ESP", "👁")
CreateSidebarButton("Hop", "🔄")
CreateSidebarButton("Info", "📊")
CreateSidebarButton("Settings", "⚙")

--======================================================
-- MOBILE RESPONSIVE
--======================================================
local function UpdateMobileLayout()
    if not workspace.CurrentCamera then return end
    local viewport = workspace.CurrentCamera.ViewportSize
    if viewport.X < 700 then
        Main.Size = UDim2.new(0.94, 0, 0.82, 0)
        Sidebar.Size = UDim2.new(0, 105, 1, -62)
        Content.Position = UDim2.fromOffset(115, 52)
        Content.Size = UDim2.new(1, -125, 1, -62)
        Title.TextSize = 16
    else
        Main.Size = UDim2.fromOffset(660, 490)
        Sidebar.Size = UDim2.new(0, 135, 1, -62)
        Content.Position = UDim2.fromOffset(145, 52)
        Content.Size = UDim2.new(1, -155, 1, -62)
        Title.TextSize = 20
    end
end

workspace.CurrentCamera:GetPropertyChangedSignal("ViewportSize"):Connect(UpdateMobileLayout)
UpdateMobileLayout()

--======================================================
-- OPEN / CLOSE
--======================================================
local Open = false

local function SetOpen(State)
    Open = State
    if State then
        Main.Visible = true
        Main.Size = UDim2.fromOffset(0, 0)
        local vp = workspace.CurrentCamera and workspace.CurrentCamera.ViewportSize
        if vp and vp.X < 700 then
            TweenService:Create(Main, TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
                Size = UDim2.new(0.94, 0, 0.82, 0)
            }):Play()
        else
            TweenService:Create(Main, TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
                Size = UDim2.fromOffset(660, 490)
            }):Play()
        end
        FloatButton.Text = "×"
    else
        Main.Visible = false
        FloatButton.Text = "N"
    end
end

FloatButton.Activated:Connect(function() SetOpen(not Open) end)
CloseButton.Activated:Connect(function() SetOpen(false) end)

ShowPage("Teleport")

print("========================================")
print("        NOVA HUB V5.2 LOADED")
print("        BLACK ANIME PREMIUM")
print("        FIX: Background Transparan")
print("        FIX: Float Button Ga Ketutup")
print("========================================")
