local player = game.Players.LocalPlayer
local ScreenGui = Instance.new("ScreenGui", player.PlayerGui)
local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0.12, 0, 0.12, 0)
MainFrame.Position = UDim2.new(0.43, 0, 0.43, 0)
MainFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
MainFrame.BorderSizePixel = 0

local UICornerFrame = Instance.new("UICorner", MainFrame)
UICornerFrame.CornerRadius = UDim.new(0, 10)

local Title = Instance.new("TextLabel", MainFrame)
Title.Size = UDim2.new(1, 0, 0.3, 0)
Title.Text = "Appraisal Menu"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 20

local StartButton = Instance.new("TextButton", MainFrame)
StartButton.Size = UDim2.new(0.9, 0, 0.25, 0)
StartButton.Position = UDim2.new(0.05, 0, 0.35, 0)
StartButton.Text = "Start Appraisal"
StartButton.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
StartButton.TextColor3 = Color3.fromRGB(255, 255, 255)
StartButton.Font = Enum.Font.SourceSans
StartButton.TextSize = 18

local UICornerStartButton = Instance.new("UICorner", StartButton)
UICornerStartButton.CornerRadius = UDim.new(0, 10)

local StopButton = Instance.new("TextButton", MainFrame)
StopButton.Size = UDim2.new(0.9, 0, 0.25, 0)
StopButton.Position = UDim2.new(0.05, 0, 0.65, 0)
StopButton.Text = "Stop Appraisal"
StopButton.BackgroundColor3 = Color3.fromRGB(170, 0, 0)
StopButton.TextColor3 = Color3.fromRGB(255, 255, 255)
StopButton.Font = Enum.Font.SourceSans
StopButton.TextSize = 18

local UICornerStopButton = Instance.new("UICorner", StopButton)
UICornerStopButton.CornerRadius = UDim.new(0, 10)

local CloseButton = Instance.new("TextButton", MainFrame)
CloseButton.Size = UDim2.new(0.08, 0, 0.12, 0)
CloseButton.Position = UDim2.new(0.88, 0, 0.02, 0)
CloseButton.Text = "X"
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Font = Enum.Font.SourceSansBold
CloseButton.TextSize = 18

local UICornerCloseButton = Instance.new("UICorner", CloseButton)
UICornerCloseButton.CornerRadius = UDim.new(0, 10)

local appraisalActive = false
local appraisalLoop

local function startAppraisal()
    if not appraisalActive then
        appraisalActive = true
        appraisalLoop = task.spawn(function()
            while appraisalActive do
                workspace.world.npcs.Appraiser.appraiser.appraise:InvokeServer()
                task.wait(0.1)
            end
        end)
    end
end

local function stopAppraisal()
    appraisalActive = false
end

local function toggleMenu()
    MainFrame.Visible = not MainFrame.Visible
end

local function exitScript()
    MainFrame:Destroy()
end

local dragging = false
local dragInput, mousePos, framePos

local function beginDrag(input)
    dragging = true
    dragInput = input
    mousePos = input.Position
    framePos = MainFrame.Position
end

local function updateDrag(input)
    if dragging then
        local delta = input.Position - mousePos
        MainFrame.Position = UDim2.new(framePos.X.Scale, framePos.X.Offset + delta.X, framePos.Y.Scale, framePos.Y.Offset + delta.Y)
    end
end

local function endDrag()
    dragging = false
end


MainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        beginDrag(input)
    end
end)

MainFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        updateDrag(input)
    end
end)

MainFrame.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        endDrag()
    end
end)

StartButton.MouseButton1Click:Connect(startAppraisal)
StopButton.MouseButton1Click:Connect(stopAppraisal)
CloseButton.MouseButton1Click:Connect(exitScript)

local UserInputService = game:GetService("UserInputService")
UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if not gameProcessedEvent and input.KeyCode == Enum.KeyCode.N then
        toggleMenu()
    end
end)
