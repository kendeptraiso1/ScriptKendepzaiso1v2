-- Tạo giao diện giả lập đáng sợ
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local Label = Instance.new("TextLabel")
local ExitButton = Instance.new("TextButton")
local TweenService = game:GetService("TweenService")

-- Cấu hình ScreenGui
ScreenGui.Name = "ScaryNotification"
ScreenGui.Parent = game.CoreGui

-- Cấu hình Frame
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.new(0, 0, 0) -- Màu đen
Frame.Size = UDim2.new(0, 300, 0, 150)
Frame.Position = UDim2.new(0.5, -150, 0.5, -75)
Frame.AnchorPoint = Vector2.new(0.5, 0.5)
Frame.BorderSizePixel = 0

-- Cấu hình Label
Label.Parent = Frame
Label.Text = "Tài khoản của bạn đã bị tôi lấy cắp!"
Label.Size = UDim2.new(1, 0, 0.8, 0)
Label.Position = UDim2.new(0, 0, 0, 0)
Label.TextColor3 = Color3.new(1, 0, 0) -- Màu đỏ
Label.BackgroundTransparency = 1
Label.Font = Enum.Font.GothamBlack
Label.TextSize = 18
Label.TextWrapped = true

-- Cấu hình ExitButton
ExitButton.Parent = Frame
ExitButton.Text = "Thoát game"
ExitButton.Size = UDim2.new(0.5, 0, 0.2, 0)
ExitButton.Position = UDim2.new(0.25, 0, 0.8, 0)
ExitButton.TextColor3 = Color3.new(1, 1, 1)
ExitButton.BackgroundColor3 = Color3.new(0.8, 0, 0) -- Màu đỏ đậm
ExitButton.Font = Enum.Font.GothamBold
ExitButton.TextSize = 16
ExitButton.Visible = false -- Ẩn nút cho đến khi hiển thị

-- Khóa toàn bộ thao tác
local function disableInput()
    local UserInputService = game:GetService("UserInputService")
    UserInputService.InputBegan:Connect(function(input)
        -- Ngăn chặn mọi phím bấm và chuột
        input.UserInputState = Enum.UserInputState.Cancel
    end)
end

-- Phóng to bảng dần dần
local function enlargeFrame()
    for i = 1, 50 do
        Frame.Size = Frame.Size + UDim2.new(0.02, 0, 0.02, 0)
        Frame.Position = UDim2.new(0.5, -Frame.Size.X.Offset / 2, 0.5, -Frame.Size.Y.Offset / 2)
        wait(0.1)
    end
end

-- Hiển thị nút "Thoát game" sau vài giây
local function showExitButton()
    wait(5) -- Chờ 5 giây
    ExitButton.Visible = true
end

-- Xử lý sự kiện khi nhấn nút "Thoát game"
ExitButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy() -- Xóa giao diện
    -- Mở link YouTube Rickroll
    local request = syn and syn.request or request or http_request
    if request then
        request({
            Url = "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
            Method = "GET"
        })
    end
    game:Shutdown() -- Giả lập thoát game
end)

-- Thực thi các hiệu ứng
disableInput() -- Khóa thao tác
spawn(enlargeFrame) -- Phóng to bảng
spawn(showExitButton) -- Hiển thị nút thoát game sau 5 giây
