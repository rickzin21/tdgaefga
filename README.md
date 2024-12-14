--abaixo estará Lib da nossa UI

local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()

local UI = Lib:Create{
    Theme = "Dark", 
    Size = UDim2.new(0, 555, 0, 400) 
 }
 
 local Main = UI:Tab{
    Name = "Inicio"
 }
 
 local Divider = Main:Divider{
    Name = "Inicio shit"
 }
 
 local QuitDivider = Main:Divider{
    Name = "Sair"
 }

 local KillAll = Divider:Button{
    Name = "anomic",
    Description = "Kills all the players in the game!",
    Callback = function()
        print("All players killed.")
    end
 }
 local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")

local active = true

local function createCrosshairCircle()
    local circle = Drawing.new("Circle")
    circle.Thickness = 2
    circle.Radius = 50
    circle.Color = Color3.fromRGB(255, 0, 0)
    circle.Filled = false

    RunService.RenderStepped:Connect(function()
        local mouse = Players.LocalPlayer:GetMouse()
        circle.Position = Vector2.new(mouse.X, mouse.Y)
        circle.Visible = active
    end)
end

local function spawnItem(Lockpick)
    if active then
        local item = ReplicatedStorage:FindFirstChild(Lockpick):Clone()
        item.Parent = workspace
        item.Position = Players.LocalPlayer.Character.HumanoidRootPart.Position + Vector3.new(0, 5, 0)
    end
end

local function toggleScript()
    active = not active
end

Players.PlayerAdded:Connect(function(player)
    createCrosshairCircle()
    player.Chatted:Connect(function(msg)
        if msg == "!spawn" then
            spawnItem("Lockpick")  
        elseif msg == "!toggle" then
            toggleScript()
        end
    end)
end)
