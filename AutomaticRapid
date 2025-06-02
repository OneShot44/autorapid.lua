--[[ 
📜 Script: Age of Heroes - Super Rapid Punch Auto (com delay configurável)
✔️ Usa o mesmo método do seu script original
✔️ Dispara múltiplos socos automaticamente a cada X segundos
✔️ Com Anti-AFK e Interface configurável
]]

-- Configuração inicial
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local VirtualUser = game:GetService("VirtualUser")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local UserInputService = game:GetService("UserInputService")
local PunchEvent = ReplicatedStorage:WaitForChild("Events"):WaitForChild("Punch")

-- Anti-AFK
player.Idled:Connect(function()
	VirtualUser:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
	VirtualUser:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
end)

-- UI Setup
local ScreenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
ScreenGui.Name = "AutoRapidPunchUI"
ScreenGui.ResetOnSpawn = false

local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 300, 0, 160)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -80)
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true

local UICorner = Instance.new("UICorner", MainFrame)
UICorner.CornerRadius = UDim.new(0, 12)

local Title = Instance.new("TextLabel", MainFrame)
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Text = "Super Rapid Punch UI"
Title.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
Title.TextColor3 = Color3.new(1,1,1)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 18

local UICorner2 = Instance.new("UICorner", Title)
UICorner2.CornerRadius = UDim.new(0, 12)

-- Toggle
local toggleButton = Instance.new("TextButton", MainFrame)
toggleButton.Size = UDim2.new(0.9, 0, 0, 40)
toggleButton.Position = UDim2.new(0.05, 0, 0, 50)
toggleButton.Text = "Enable Auto Rapid Punch"
toggleButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
toggleButton.TextColor3 = Color3.new(1,1,1)
toggleButton.Font = Enum.Font.Gotham
toggleButton.TextSize = 16
local toggleCorner = Instance.new("UICorner", toggleButton)
toggleCorner.CornerRadius = UDim.new(0, 8)

-- Delay input
local delayBox = Instance.new("TextBox", MainFrame)
delayBox.Size = UDim2.new(0.9, 0, 0, 30)
delayBox.Position = UDim2.new(0.05, 0, 0, 100)
delayBox.PlaceholderText = "Delay in seconds (e.g. 2)"
delayBox.Text = "2"
delayBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
delayBox.TextColor3 = Color3.new(1,1,1)
delayBox.Font = Enum.Font.Gotham
delayBox.TextSize = 14
local delayCorner = Instance.new("UICorner", delayBox)
delayCorner.CornerRadius = UDim.new(0, 8)

-- Funcionalidade
local running = false

local function spamPunch()
	for i = 1, 10 do
		PunchEvent:FireServer(0, 0.1, 1)
	end
end

toggleButton.MouseButton1Click:Connect(function()
	running = not running
	toggleButton.Text = running and "Disable Auto Rapid Punch" or "Enable Auto Rapid Punch"

	if running then
		task.spawn(function()
			while running do
				spamPunch()
				local delay = tonumber(delayBox.Text) or 2
				task.wait(delay)
			end
		end)
	end
end)

-- Minimizar com END
local minimized = false
UserInputService.InputEnded:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.End then
		minimized = not minimized
		MainFrame.Visible = not minimized
	end
end)
