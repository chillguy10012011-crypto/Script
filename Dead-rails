

-- [HTTPGET #1]: https://raw.githubusercontent.com/SynvextiaHub/Deadrails/main/script
loadstring(game:HttpGet("https://raw.githubusercontent.com/SynvextiaHub/Loader/main/Syn"))()



-- [LOADSTRING #2] - Chunk: nil
loadstring(game:HttpGet("https://raw.githubusercontent.com/SynvextiaHub/Loader/main/Syn"))()



-- [HTTPGET #3]: https://raw.githubusercontent.com/SynvextiaHub/Loader/main/Syn
loadstring(game:HttpGet("https://raw.githubusercontent.com/SynvextiaHub/Loader./main/SYN"))()



-- [LOADSTRING #4] - Chunk: nil
loadstring(game:HttpGet("https://raw.githubusercontent.com/SynvextiaHub/Loader./main/SYN"))()



-- [HTTPGET #5]: https://raw.githubusercontent.com/SynvextiaHub/Loader./main/SYN
--[[
  Synvextia Key System -> per-game loader
  Key: syn2
  Preserves request-first fetch and task.spawn execution.
]]

print("[Synvextia] loader v2 (direct per-game URLs)")

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local GuiService = game:GetService("GuiService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local INVITE = "https://discord.gg/6YQagDhEqy"
local MESSAGE = "Join the server to get your key\nThere is no checkpoints"
local VALID_KEYS = {
    ["syn2"] = true,
}

local KEY_FILE = "synvextia_key.txt"

local function normalizeKey(s)
    return tostring(s or ""):gsub("%s+", "")
end

-- [NOTE] Some builds read getgenv().SCRIPT_KEY; set both names for compatibility.
local function saveKey(key)
    key = normalizeKey(key)
    if key == "" then return end
    pcall(function()
        if writefile then writefile(KEY_FILE, key) end
    end)
    pcall(function()
        getgenv().SCRIPT_KEY = key
        getgenv().SynvextiaKey = key
    end)
    pcall(function()
        _G.SCRIPT_KEY = key
        _G.SynvextiaKey = key
    end)
end

local function loadSavedKey()
    if typeof(isfile) == "function" and typeof(readfile) == "function" then
        local ok, is = pcall(function() return isfile(KEY_FILE) end)
        if ok and is then
            local ok2, contents = pcall(function() return readfile(KEY_FILE) end)
            if ok2 and contents then
                local k = normalizeKey(contents)
                if k ~= "" then return k end
            end
        end
    end
    if typeof(getgenv) == "function" then
        local ok, k = pcall(function() return getgenv().SCRIPT_KEY or getgenv().SynvextiaKey end)
        if ok and k and normalizeKey(k) ~= "" then return normalizeKey(k) end
    end
    if _G.SynvextiaKey and normalizeKey(_G.SynvextiaKey) ~= "" then
        return normalizeKey(_G.SynvextiaKey)
    end
    return ""
end

local function clearSavedKey()
    pcall(function()
        if typeof(delfile) == "function" and typeof(isfile) == "function" then
            if isfile(KEY_FILE) then delfile(KEY_FILE) end
        elseif writefile then
            writefile(KEY_FILE, "")
        end
    end)
    pcall(function() getgenv().SCRIPT_KEY = nil end)
    pcall(function() _G.SynvextiaKey = nil end)
end

local COL_BG_TOP = Color3.fromRGB(24, 25, 32)
local COL_BG_BOTTOM = Color3.fromRGB(12, 12, 17)
local COL_PANEL_TOP = Color3.fromRGB(48, 50, 58)
local COL_PANEL_BOTTOM = Color3.fromRGB(34, 36, 42)
local COL_ACCENT = Color3.fromRGB(88, 101, 242)
local COL_ACCENT_HOVER = Color3.fromRGB(108, 120, 255)
local COL_SUCCESS = Color3.fromRGB(35, 134, 78)
local COL_ERROR = Color3.fromRGB(178, 58, 72)
local COL_TEXT = Color3.fromRGB(245, 246, 250)
local COL_SUBTEXT = Color3.fromRGB(160, 165, 185)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "SynvextiaKeySystem"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 9999
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

local overlay = Instance.new("Frame")
overlay.Name = "Overlay"
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = COL_BG_BOTTOM
overlay.BackgroundTransparency = 1
overlay.BorderSizePixel = 0
overlay.ZIndex = 1
overlay.Parent = screenGui

local backdropGradient = Instance.new("UIGradient")
backdropGradient.Color = ColorSequence.new(COL_BG_TOP, COL_BG_BOTTOM)
backdropGradient.Rotation = 45
backdropGradient.Parent = overlay
TweenService:Create(overlay, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), { BackgroundTransparency = 0.25 }):Play()

local panel = Instance.new("Frame")
panel.Name = "Panel"
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Position = UDim2.fromScale(0.5, 0.5)
panel.Size = UDim2.new(0.9, 0, 0, 420)
panel.BackgroundColor3 = COL_PANEL_BOTTOM
panel.BorderSizePixel = 0
panel.ZIndex = 2
panel.Parent = overlay

local panelSize = Instance.new("UISizeConstraint")
panelSize.MaxSize = Vector2.new(660, 420)
panelSize.MinSize = Vector2.new(300, 420)
panelSize.Parent = panel

local panelGradient = Instance.new("UIGradient")
panelGradient.Color = ColorSequence.new(COL_PANEL_TOP, COL_PANEL_BOTTOM)
panelGradient.Rotation = 90
panelGradient.Parent = panel

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 18)
panelCorner.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Color = Color3.fromRGB(255, 255, 255)
panelStroke.Transparency = 0.85
panelStroke.Thickness = 1.5
panelStroke.Parent = panel

local accent = Instance.new("Frame")
accent.Name = "Accent"
accent.Size = UDim2.new(1, -80, 0, 6)
accent.Position = UDim2.new(0.5, 0, 0, 24)
accent.AnchorPoint = Vector2.new(0.5, 0)
accent.BackgroundColor3 = COL_ACCENT
accent.BorderSizePixel = 0
accent.ZIndex = 3
accent.Parent = panel
Instance.new("UICorner", accent).CornerRadius = UDim.new(1, 0)

local accentGradient = Instance.new("UIGradient")
accentGradient.Color = ColorSequence.new(Color3.fromRGB(120, 130, 255), COL_ACCENT)
accentGradient.Parent = accent

local wordmark = Instance.new("TextLabel")
wordmark.Name = "Wordmark"
wordmark.AnchorPoint = Vector2.new(0.5, 0)
wordmark.Position = UDim2.new(0.5, 0, 0, 44)
wordmark.Size = UDim2.new(1, -40, 0, 18)
wordmark.BackgroundTransparency = 1
wordmark.Text = "S Y N V E X T I A"
wordmark.TextColor3 = COL_ACCENT_HOVER
wordmark.TextSize = 14
wordmark.Font = Enum.Font.GothamBold
wordmark.TextTransparency = 0.25
wordmark.ZIndex = 3
wordmark.Parent = panel

local title = Instance.new("TextLabel")
title.Name = "Title"
title.AnchorPoint = Vector2.new(0.5, 0)
title.Position = UDim2.new(0.5, 0, 0, 70)
title.Size = UDim2.new(1, -50, 0, 40)
title.BackgroundTransparency = 1
title.Text = "Key System"
title.TextColor3 = COL_TEXT
title.TextSize = 30
title.Font = Enum.Font.GothamBold
title.ZIndex = 3
title.Parent = panel

local message = Instance.new("TextLabel")
message.Name = "Message"
message.AnchorPoint = Vector2.new(0.5, 0)
message.Position = UDim2.new(0.5, 0, 0, 108)
message.Size = UDim2.new(1, -50, 0, 52)
message.BackgroundTransparency = 1
message.Text = MESSAGE
message.TextColor3 = COL_SUBTEXT
message.TextWrapped = true
message.TextSize = 16
message.Font = Enum.Font.Gotham
message.TextXAlignment = Enum.TextXAlignment.Center
message.ZIndex = 3
message.Parent = panel

local joinButton = Instance.new("TextButton")
joinButton.Name = "JoinButton"
joinButton.AnchorPoint = Vector2.new(0.5, 0)
joinButton.Position = UDim2.new(0.5, 0, 0, 164)
joinButton.Size = UDim2.new(1, -100, 0, 50)
joinButton.BackgroundColor3 = COL_ACCENT
joinButton.BorderSizePixel = 0
joinButton.Text = "Copy Discord Invite"
joinButton.TextColor3 = Color3.new(1, 1, 1)
joinButton.TextSize = 22
joinButton.Font = Enum.Font.GothamBold
joinButton.AutoButtonColor = false
joinButton.ZIndex = 3
joinButton.Parent = panel
Instance.new("UICorner", joinButton).CornerRadius = UDim.new(0, 14)

local joinGradient = Instance.new("UIGradient")
joinGradient.Color = ColorSequence.new(COL_ACCENT_HOVER, COL_ACCENT)
joinGradient.Rotation = 90
joinGradient.Parent = joinButton

local joinScale = Instance.new("UIScale")
joinScale.Parent = joinButton
joinButton.MouseEnter:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
joinButton.MouseLeave:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local keyBox = Instance.new("TextBox")
keyBox.Name = "KeyBox"
keyBox.AnchorPoint = Vector2.new(0.5, 0)
keyBox.Position = UDim2.new(0.5, 0, 0, 236)
keyBox.Size = UDim2.new(1, -110, 0, 42)
keyBox.BackgroundColor3 = Color3.fromRGB(20, 21, 26)
keyBox.BackgroundTransparency = 0.25
keyBox.BorderSizePixel = 0
keyBox.ClearTextOnFocus = false
keyBox.Font = Enum.Font.Code
keyBox.PlaceholderText = "Paste your key here..."
keyBox.Text = ""
keyBox.TextColor3 = COL_TEXT
keyBox.PlaceholderColor3 = COL_SUBTEXT
keyBox.TextSize = 16
keyBox.TextXAlignment = Enum.TextXAlignment.Center
keyBox.ZIndex = 3
keyBox.Parent = panel
Instance.new("UICorner", keyBox).CornerRadius = UDim.new(0, 8)

local checkButton = Instance.new("TextButton")
checkButton.Name = "CheckButton"
checkButton.AnchorPoint = Vector2.new(0.5, 0)
checkButton.Position = UDim2.new(0.5, 0, 0, 296)
checkButton.Size = UDim2.new(1, -100, 0, 50)
checkButton.BackgroundColor3 = COL_SUCCESS
checkButton.BorderSizePixel = 0
checkButton.Text = "Check Key"
checkButton.TextColor3 = Color3.new(1, 1, 1)
checkButton.TextSize = 22
checkButton.Font = Enum.Font.GothamBold
checkButton.AutoButtonColor = false
checkButton.ZIndex = 3
checkButton.Parent = panel
Instance.new("UICorner", checkButton).CornerRadius = UDim.new(0, 14)

local checkScale = Instance.new("UIScale")
checkScale.Parent = checkButton
checkButton.MouseEnter:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
checkButton.MouseLeave:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local status = Instance.new("TextLabel")
status.Name = "Status"
status.AnchorPoint = Vector2.new(0.5, 0)
status.Position = UDim2.new(0.5, 0, 0, 360)
status.Size = UDim2.new(1, -40, 0, 20)
status.BackgroundTransparency = 1
status.Text = ""
status.TextColor3 = COL_SUBTEXT
status.TextSize = 14
status.Font = Enum.Font.Gotham
status.ZIndex = 3
status.Parent = panel

local busy = false
local accepted = false
local launchRequest = nil

-- [LOADER] Request-first fetch, then game:HttpGet fallback.
local function fetch(url)
    local req = (type(syn) == "table" and syn.request) or request or http_request
    if type(req) == "function" then
        local ok, res = pcall(req, { Url = url, Method = "GET" })
        if ok and type(res) == "table" and tonumber(res.StatusCode) == 200 and type(res.Body) == "string" and res.Body ~= "" then
            return res.Body
        end
    end

    local ok, source = pcall(game.HttpGet, game, url)
    if ok and type(source) == "string" and source ~= "" then
        return source
    end

    return nil
end

local SCRIPTS = {
    MM2        = "https://api.jnkie.com/api/v1/luascripts/public/f88bc27f071600baaa1afc246ffb6c53461c215a7db93c969959072152943cd5/download",
    DOORS      = "https://api.jnkie.com/api/v1/luascripts/public/7915991c0c868d1938aff55d370c8050e063cbcb8762a95fd405f21b8587ea2c/download",
    TIMEBOMB   = "https://api.jnkie.com/api/v1/luascripts/public/69a06a1de9966f3012fb2bd2cb8d5d2af674dc9125f4d0ba7b4fd323a8dce635/download",
    FORSAKEN   = "https://api.jnkie.com/api/v1/luascripts/public/7c4032d89f36d9fab5ac0076a4802086eebc9d17c223283ea042bc9753ebd2cc/download",
    DEADRAILS  = "https://api.jnkie.com/api/v1/luascripts/public/19ab1970bbdf3b967d63349f52d7967b0e7a39860a4e463f2f4771a165aa543e/download",
    VOLLEYBALL = "https://api.jnkie.com/api/v1/luascripts/public/41bf8158fc125b3d895f332771b5aeaed072c5b8ea16d8002d0878644fa3578f/download",
    NIGHTS99   = "https://api.jnkie.com/api/v1/luascripts/public/1238dbd70c6f460836b85fca2e3311debed55047f9e21b8207de07caf7867d0f/download",
    HUSSVALLEY = "https://api.jnkie.com/api/v1/luascripts/public/fafaa6d66f82d1f8448f07b70e342014c18adc491dda695c13c0547776342f7e/download",
}

local byGameId = {
    [6931042565] = SCRIPTS.VOLLEYBALL,
    [2440500124] = SCRIPTS.DOORS,
}

local byPlaceId = {
    -- Murder Mystery 2
    [142823291] = SCRIPTS.MM2,
    [335132309] = SCRIPTS.MM2,
    [636649648] = SCRIPTS.MM2,
    [80469437126309] = SCRIPTS.MM2,

    -- DOORS
    [6516141723] = SCRIPTS.DOORS,
    [6839171747] = SCRIPTS.DOORS,
    [10549820578] = SCRIPTS.DOORS,
    [12308344607] = SCRIPTS.DOORS,
    [87716067947993] = SCRIPTS.DOORS,
    [110258689672367] = SCRIPTS.DOORS,

    -- Timebomb Duels
    [11379739543] = SCRIPTS.TIMEBOMB,

    -- Forsaken
    [18687417158] = SCRIPTS.FORSAKEN,
    [83645629621104] = SCRIPTS.FORSAKEN,
    [86454545238517] = SCRIPTS.FORSAKEN,
    [94626476208514] = SCRIPTS.FORSAKEN,
    [106560117662077] = SCRIPTS.FORSAKEN,

    -- Dead Rails
    [70876832253163] = SCRIPTS.DEADRAILS,
    [74106709399219] = SCRIPTS.DEADRAILS,
    [96831577561553] = SCRIPTS.DEADRAILS,
    [110282088381749] = SCRIPTS.DEADRAILS,
    [111285651581407] = SCRIPTS.DEADRAILS,
    [116495829188952] = SCRIPTS.DEADRAILS,

    -- Volleyball Legends
    [73956553001240] = SCRIPTS.VOLLEYBALL,
    [74691681039273] = SCRIPTS.VOLLEYBALL,
    [85395484560711] = SCRIPTS.VOLLEYBALL,
    [86789627188240] = SCRIPTS.VOLLEYBALL,
    [96802054849934] = SCRIPTS.VOLLEYBALL,
    [102580589030177] = SCRIPTS.VOLLEYBALL,
    [103521881639626] = SCRIPTS.VOLLEYBALL,
    [109684591839194] = SCRIPTS.VOLLEYBALL,
    [117134837736236] = SCRIPTS.VOLLEYBALL,
    [134314141048307] = SCRIPTS.VOLLEYBALL,

    -- 99 Nights in the Forest
    [79546208627805] = SCRIPTS.NIGHTS99,
    [126509999114328] = SCRIPTS.NIGHTS99,

    -- Huss Valley
    [107535308163741] = SCRIPTS.HUSSVALLEY,
}

local function getScriptUrl()
    local gameId = game.GameId
    while gameId == 0 and game.PlaceId == 0 do
        task.wait()
        gameId = game.GameId
    end
    return byGameId[gameId] or byPlaceId[game.PlaceId]
end

-- Returns the payload source, or nil plus a message for the UI.
local function deliver(key)
    local url = getScriptUrl()
    if not url then
        return nil, ("Unsupported game. PlaceId=%s GameId=%s"):format(tostring(game.PlaceId), tostring(game.GameId))
    end

    status.Text = "Downloading script..."
    for attempt = 1, 3 do
        local source = fetch(url)
        if source then return source end
        task.wait(0.5)
    end

    return nil, "Could not download the script. Check your connection or executor."
end

-- [LOADER] The main thread waits for the key UI, then fetches and compiles the
--  payload. The payload itself runs in task.spawn so the Continue button and
--  the rest of the game thread are not blocked.
local function runLaunch()
    while true do
        while not launchRequest do
            task.wait(0.1)
        end

        local key = launchRequest
        launchRequest = nil

        status.Text = "Loading Synvextia..."
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Loading"

        local started = os.clock()
        local okCall, payload, err = pcall(deliver, key)
        if not okCall then
            payload, err = nil, tostring(payload)
        end

        if not payload then
            -- keep the UI alive so the key can be retried
            accepted = false
            status.Text = tostring(err or "Loader error")
            status.TextColor3 = COL_ERROR
            checkButton.Text = "Check Key"
            warn("[Synvextia] " .. tostring(err))
        else
            print(("[Synvextia] payload: %d bytes in %.1fs"):format(#payload, os.clock() - started))

            local chunk, compileErr = loadstring(payload)
            if not chunk then
                accepted = false
                status.Text = "Loader script failed to compile"
                status.TextColor3 = COL_ERROR
                checkButton.Text = "Check Key"
                warn("[Synvextia] compile error: " .. tostring(compileErr))
            else
                pcall(function() screenGui:Destroy() end)

                -- Let the pulse loop and any click/auto-login thread finish
                -- before spawning the payload thread.
                task.wait(0.3)

                task.spawn(function()
                    local okRun, runErr = pcall(chunk)
                    if okRun then
                        print(("[Synvextia] loader returned after %.1fs"):format(os.clock() - started))
                    else
                        warn(("[Synvextia] loader failed after %.1fs: %s"):format(os.clock() - started, tostring(runErr)))
                    end
                end)
                break
            end
        end
    end
end

local function checkKey(isAuto)
    if accepted then return end
    local key = normalizeKey(keyBox.Text)
    if key == "" then
        if not isAuto then
            status.Text = "Enter a key first"
            status.TextColor3 = COL_ERROR
        end
        return
    end
    -- [NOTE] Local key check.
    if VALID_KEYS[key] then
        accepted = true
        saveKey(key)
        status.Text = isAuto and "Saved key found! Logging in..." or "Key accepted!"
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Success"
        task.wait(0.6)
        launchRequest = key
    else
        status.Text = "Invalid key - join the server for one"
        status.TextColor3 = COL_ERROR
        if isAuto then
            clearSavedKey()
            keyBox.Text = ""
        end
    end
end

joinButton.MouseButton1Click:Connect(function()
    if busy then return end
    busy = true
    local copied = false
    local fns = {}
    if typeof(setclipboard) == "function" then table.insert(fns, setclipboard) end
    if typeof(writeclipboard) == "function" then table.insert(fns, writeclipboard) end
    table.insert(fns, function(t) return GuiService:SetClipboard(t) end)

    for _, fn in ipairs(fns) do
        local ok = pcall(fn, INVITE)
        if ok then copied = true break end
    end
    if not copied then
        keyBox.Text = INVITE
    end
    joinButton.Text = copied and "Copied! Paste in Discord" or "Invite in box - copy it"
    task.wait(1.8)
    joinButton.Text = "Copy Discord Invite"
    busy = false
end)

checkButton.MouseButton1Click:Connect(function() checkKey(false) end)
keyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then checkKey(false) end
end)

local lastAuto = 0
keyBox:GetPropertyChangedSignal("Text"):Connect(function()
    if accepted then return end
    local k = normalizeKey(keyBox.Text)
    if VALID_KEYS[k] and tick() - lastAuto > 1 then
        lastAuto = tick()
        checkKey(false)
    end
end)

task.spawn(function()
    local saved = loadSavedKey()
    if saved ~= "" then
        keyBox.Text = saved
        status.Text = "Saved key found! Logging in..."
        status.TextColor3 = COL_SUBTEXT
        task.wait(0.6)
        if not screenGui.Parent then return end
        checkKey(true)
    end
end)

task.spawn(function()
    while screenGui.Parent do
        local pulse = math.sin(tick() * 2) * 0.5 + 0.5
        joinGradient.Offset = Vector2.new(0, pulse * 0.6 - 0.3)
        RunService.RenderStepped:Wait()
    end
end)

-- The main thread waits for the key UI, then fetches and compiles the payload.
-- The payload runs in task.spawn so it does not block the UI or game thread.
runLaunch()



-- [LOADSTRING #6] - Chunk: nil
--[[
  Synvextia Key System -> per-game loader
  Key: syn2
  Preserves request-first fetch and task.spawn execution.
]]

print("[Synvextia] loader v2 (direct per-game URLs)")

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local GuiService = game:GetService("GuiService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local INVITE = "https://discord.gg/6YQagDhEqy"
local MESSAGE = "Join the server to get your key\nThere is no checkpoints"
local VALID_KEYS = {
    ["syn2"] = true,
}

local KEY_FILE = "synvextia_key.txt"

local function normalizeKey(s)
    return tostring(s or ""):gsub("%s+", "")
end

-- [NOTE] Some builds read getgenv().SCRIPT_KEY; set both names for compatibility.
local function saveKey(key)
    key = normalizeKey(key)
    if key == "" then return end
    pcall(function()
        if writefile then writefile(KEY_FILE, key) end
    end)
    pcall(function()
        getgenv().SCRIPT_KEY = key
        getgenv().SynvextiaKey = key
    end)
    pcall(function()
        _G.SCRIPT_KEY = key
        _G.SynvextiaKey = key
    end)
end

local function loadSavedKey()
    if typeof(isfile) == "function" and typeof(readfile) == "function" then
        local ok, is = pcall(function() return isfile(KEY_FILE) end)
        if ok and is then
            local ok2, contents = pcall(function() return readfile(KEY_FILE) end)
            if ok2 and contents then
                local k = normalizeKey(contents)
                if k ~= "" then return k end
            end
        end
    end
    if typeof(getgenv) == "function" then
        local ok, k = pcall(function() return getgenv().SCRIPT_KEY or getgenv().SynvextiaKey end)
        if ok and k and normalizeKey(k) ~= "" then return normalizeKey(k) end
    end
    if _G.SynvextiaKey and normalizeKey(_G.SynvextiaKey) ~= "" then
        return normalizeKey(_G.SynvextiaKey)
    end
    return ""
end

local function clearSavedKey()
    pcall(function()
        if typeof(delfile) == "function" and typeof(isfile) == "function" then
            if isfile(KEY_FILE) then delfile(KEY_FILE) end
        elseif writefile then
            writefile(KEY_FILE, "")
        end
    end)
    pcall(function() getgenv().SCRIPT_KEY = nil end)
    pcall(function() _G.SynvextiaKey = nil end)
end

local COL_BG_TOP = Color3.fromRGB(24, 25, 32)
local COL_BG_BOTTOM = Color3.fromRGB(12, 12, 17)
local COL_PANEL_TOP = Color3.fromRGB(48, 50, 58)
local COL_PANEL_BOTTOM = Color3.fromRGB(34, 36, 42)
local COL_ACCENT = Color3.fromRGB(88, 101, 242)
local COL_ACCENT_HOVER = Color3.fromRGB(108, 120, 255)
local COL_SUCCESS = Color3.fromRGB(35, 134, 78)
local COL_ERROR = Color3.fromRGB(178, 58, 72)
local COL_TEXT = Color3.fromRGB(245, 246, 250)
local COL_SUBTEXT = Color3.fromRGB(160, 165, 185)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "SynvextiaKeySystem"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 9999
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

local overlay = Instance.new("Frame")
overlay.Name = "Overlay"
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = COL_BG_BOTTOM
overlay.BackgroundTransparency = 1
overlay.BorderSizePixel = 0
overlay.ZIndex = 1
overlay.Parent = screenGui

local backdropGradient = Instance.new("UIGradient")
backdropGradient.Color = ColorSequence.new(COL_BG_TOP, COL_BG_BOTTOM)
backdropGradient.Rotation = 45
backdropGradient.Parent = overlay
TweenService:Create(overlay, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), { BackgroundTransparency = 0.25 }):Play()

local panel = Instance.new("Frame")
panel.Name = "Panel"
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Position = UDim2.fromScale(0.5, 0.5)
panel.Size = UDim2.new(0.9, 0, 0, 420)
panel.BackgroundColor3 = COL_PANEL_BOTTOM
panel.BorderSizePixel = 0
panel.ZIndex = 2
panel.Parent = overlay

local panelSize = Instance.new("UISizeConstraint")
panelSize.MaxSize = Vector2.new(660, 420)
panelSize.MinSize = Vector2.new(300, 420)
panelSize.Parent = panel

local panelGradient = Instance.new("UIGradient")
panelGradient.Color = ColorSequence.new(COL_PANEL_TOP, COL_PANEL_BOTTOM)
panelGradient.Rotation = 90
panelGradient.Parent = panel

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 18)
panelCorner.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Color = Color3.fromRGB(255, 255, 255)
panelStroke.Transparency = 0.85
panelStroke.Thickness = 1.5
panelStroke.Parent = panel

local accent = Instance.new("Frame")
accent.Name = "Accent"
accent.Size = UDim2.new(1, -80, 0, 6)
accent.Position = UDim2.new(0.5, 0, 0, 24)
accent.AnchorPoint = Vector2.new(0.5, 0)
accent.BackgroundColor3 = COL_ACCENT
accent.BorderSizePixel = 0
accent.ZIndex = 3
accent.Parent = panel
Instance.new("UICorner", accent).CornerRadius = UDim.new(1, 0)

local accentGradient = Instance.new("UIGradient")
accentGradient.Color = ColorSequence.new(Color3.fromRGB(120, 130, 255), COL_ACCENT)
accentGradient.Parent = accent

local wordmark = Instance.new("TextLabel")
wordmark.Name = "Wordmark"
wordmark.AnchorPoint = Vector2.new(0.5, 0)
wordmark.Position = UDim2.new(0.5, 0, 0, 44)
wordmark.Size = UDim2.new(1, -40, 0, 18)
wordmark.BackgroundTransparency = 1
wordmark.Text = "S Y N V E X T I A"
wordmark.TextColor3 = COL_ACCENT_HOVER
wordmark.TextSize = 14
wordmark.Font = Enum.Font.GothamBold
wordmark.TextTransparency = 0.25
wordmark.ZIndex = 3
wordmark.Parent = panel

local title = Instance.new("TextLabel")
title.Name = "Title"
title.AnchorPoint = Vector2.new(0.5, 0)
title.Position = UDim2.new(0.5, 0, 0, 70)
title.Size = UDim2.new(1, -50, 0, 40)
title.BackgroundTransparency = 1
title.Text = "Key System"
title.TextColor3 = COL_TEXT
title.TextSize = 30
title.Font = Enum.Font.GothamBold
title.ZIndex = 3
title.Parent = panel

local message = Instance.new("TextLabel")
message.Name = "Message"
message.AnchorPoint = Vector2.new(0.5, 0)
message.Position = UDim2.new(0.5, 0, 0, 108)
message.Size = UDim2.new(1, -50, 0, 52)
message.BackgroundTransparency = 1
message.Text = MESSAGE
message.TextColor3 = COL_SUBTEXT
message.TextWrapped = true
message.TextSize = 16
message.Font = Enum.Font.Gotham
message.TextXAlignment = Enum.TextXAlignment.Center
message.ZIndex = 3
message.Parent = panel

local joinButton = Instance.new("TextButton")
joinButton.Name = "JoinButton"
joinButton.AnchorPoint = Vector2.new(0.5, 0)
joinButton.Position = UDim2.new(0.5, 0, 0, 164)
joinButton.Size = UDim2.new(1, -100, 0, 50)
joinButton.BackgroundColor3 = COL_ACCENT
joinButton.BorderSizePixel = 0
joinButton.Text = "Copy Discord Invite"
joinButton.TextColor3 = Color3.new(1, 1, 1)
joinButton.TextSize = 22
joinButton.Font = Enum.Font.GothamBold
joinButton.AutoButtonColor = false
joinButton.ZIndex = 3
joinButton.Parent = panel
Instance.new("UICorner", joinButton).CornerRadius = UDim.new(0, 14)

local joinGradient = Instance.new("UIGradient")
joinGradient.Color = ColorSequence.new(COL_ACCENT_HOVER, COL_ACCENT)
joinGradient.Rotation = 90
joinGradient.Parent = joinButton

local joinScale = Instance.new("UIScale")
joinScale.Parent = joinButton
joinButton.MouseEnter:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
joinButton.MouseLeave:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local keyBox = Instance.new("TextBox")
keyBox.Name = "KeyBox"
keyBox.AnchorPoint = Vector2.new(0.5, 0)
keyBox.Position = UDim2.new(0.5, 0, 0, 236)
keyBox.Size = UDim2.new(1, -110, 0, 42)
keyBox.BackgroundColor3 = Color3.fromRGB(20, 21, 26)
keyBox.BackgroundTransparency = 0.25
keyBox.BorderSizePixel = 0
keyBox.ClearTextOnFocus = false
keyBox.Font = Enum.Font.Code
keyBox.PlaceholderText = "Paste your key here..."
keyBox.Text = ""
keyBox.TextColor3 = COL_TEXT
keyBox.PlaceholderColor3 = COL_SUBTEXT
keyBox.TextSize = 16
keyBox.TextXAlignment = Enum.TextXAlignment.Center
keyBox.ZIndex = 3
keyBox.Parent = panel
Instance.new("UICorner", keyBox).CornerRadius = UDim.new(0, 8)

local checkButton = Instance.new("TextButton")
checkButton.Name = "CheckButton"
checkButton.AnchorPoint = Vector2.new(0.5, 0)
checkButton.Position = UDim2.new(0.5, 0, 0, 296)
checkButton.Size = UDim2.new(1, -100, 0, 50)
checkButton.BackgroundColor3 = COL_SUCCESS
checkButton.BorderSizePixel = 0
checkButton.Text = "Check Key"
checkButton.TextColor3 = Color3.new(1, 1, 1)
checkButton.TextSize = 22
checkButton.Font = Enum.Font.GothamBold
checkButton.AutoButtonColor = false
checkButton.ZIndex = 3
checkButton.Parent = panel
Instance.new("UICorner", checkButton).CornerRadius = UDim.new(0, 14)

local checkScale = Instance.new("UIScale")
checkScale.Parent = checkButton
checkButton.MouseEnter:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
checkButton.MouseLeave:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local status = Instance.new("TextLabel")
status.Name = "Status"
status.AnchorPoint = Vector2.new(0.5, 0)
status.Position = UDim2.new(0.5, 0, 0, 360)
status.Size = UDim2.new(1, -40, 0, 20)
status.BackgroundTransparency = 1
status.Text = ""
status.TextColor3 = COL_SUBTEXT
status.TextSize = 14
status.Font = Enum.Font.Gotham
status.ZIndex = 3
status.Parent = panel

local busy = false
local accepted = false
local launchRequest = nil

-- [LOADER] Request-first fetch, then game:HttpGet fallback.
local function fetch(url)
    local req = (type(syn) == "table" and syn.request) or request or http_request
    if type(req) == "function" then
        local ok, res = pcall(req, { Url = url, Method = "GET" })
        if ok and type(res) == "table" and tonumber(res.StatusCode) == 200 and type(res.Body) == "string" and res.Body ~= "" then
            return res.Body
        end
    end

    local ok, source = pcall(game.HttpGet, game, url)
    if ok and type(source) == "string" and source ~= "" then
        return source
    end

    return nil
end

local SCRIPTS = {
    MM2        = "https://api.jnkie.com/api/v1/luascripts/public/f88bc27f071600baaa1afc246ffb6c53461c215a7db93c969959072152943cd5/download",
    DOORS      = "https://api.jnkie.com/api/v1/luascripts/public/7915991c0c868d1938aff55d370c8050e063cbcb8762a95fd405f21b8587ea2c/download",
    TIMEBOMB   = "https://api.jnkie.com/api/v1/luascripts/public/69a06a1de9966f3012fb2bd2cb8d5d2af674dc9125f4d0ba7b4fd323a8dce635/download",
    FORSAKEN   = "https://api.jnkie.com/api/v1/luascripts/public/7c4032d89f36d9fab5ac0076a4802086eebc9d17c223283ea042bc9753ebd2cc/download",
    DEADRAILS  = "https://api.jnkie.com/api/v1/luascripts/public/19ab1970bbdf3b967d63349f52d7967b0e7a39860a4e463f2f4771a165aa543e/download",
    VOLLEYBALL = "https://api.jnkie.com/api/v1/luascripts/public/41bf8158fc125b3d895f332771b5aeaed072c5b8ea16d8002d0878644fa3578f/download",
    NIGHTS99   = "https://api.jnkie.com/api/v1/luascripts/public/1238dbd70c6f460836b85fca2e3311debed55047f9e21b8207de07caf7867d0f/download",
    HUSSVALLEY = "https://api.jnkie.com/api/v1/luascripts/public/fafaa6d66f82d1f8448f07b70e342014c18adc491dda695c13c0547776342f7e/download",
}

local byGameId = {
    [6931042565] = SCRIPTS.VOLLEYBALL,
    [2440500124] = SCRIPTS.DOORS,
}

local byPlaceId = {
    -- Murder Mystery 2
    [142823291] = SCRIPTS.MM2,
    [335132309] = SCRIPTS.MM2,
    [636649648] = SCRIPTS.MM2,
    [80469437126309] = SCRIPTS.MM2,

    -- DOORS
    [6516141723] = SCRIPTS.DOORS,
    [6839171747] = SCRIPTS.DOORS,
    [10549820578] = SCRIPTS.DOORS,
    [12308344607] = SCRIPTS.DOORS,
    [87716067947993] = SCRIPTS.DOORS,
    [110258689672367] = SCRIPTS.DOORS,

    -- Timebomb Duels
    [11379739543] = SCRIPTS.TIMEBOMB,

    -- Forsaken
    [18687417158] = SCRIPTS.FORSAKEN,
    [83645629621104] = SCRIPTS.FORSAKEN,
    [86454545238517] = SCRIPTS.FORSAKEN,
    [94626476208514] = SCRIPTS.FORSAKEN,
    [106560117662077] = SCRIPTS.FORSAKEN,

    -- Dead Rails
    [70876832253163] = SCRIPTS.DEADRAILS,
    [74106709399219] = SCRIPTS.DEADRAILS,
    [96831577561553] = SCRIPTS.DEADRAILS,
    [110282088381749] = SCRIPTS.DEADRAILS,
    [111285651581407] = SCRIPTS.DEADRAILS,
    [116495829188952] = SCRIPTS.DEADRAILS,

    -- Volleyball Legends
    [73956553001240] = SCRIPTS.VOLLEYBALL,
    [74691681039273] = SCRIPTS.VOLLEYBALL,
    [85395484560711] = SCRIPTS.VOLLEYBALL,
    [86789627188240] = SCRIPTS.VOLLEYBALL,
    [96802054849934] = SCRIPTS.VOLLEYBALL,
    [102580589030177] = SCRIPTS.VOLLEYBALL,
    [103521881639626] = SCRIPTS.VOLLEYBALL,
    [109684591839194] = SCRIPTS.VOLLEYBALL,
    [117134837736236] = SCRIPTS.VOLLEYBALL,
    [134314141048307] = SCRIPTS.VOLLEYBALL,

    -- 99 Nights in the Forest
    [79546208627805] = SCRIPTS.NIGHTS99,
    [126509999114328] = SCRIPTS.NIGHTS99,

    -- Huss Valley
    [107535308163741] = SCRIPTS.HUSSVALLEY,
}

local function getScriptUrl()
    local gameId = game.GameId
    while gameId == 0 and game.PlaceId == 0 do
        task.wait()
        gameId = game.GameId
    end
    return byGameId[gameId] or byPlaceId[game.PlaceId]
end

-- Returns the payload source, or nil plus a message for the UI.
local function deliver(key)
    local url = getScriptUrl()
    if not url then
        return nil, ("Unsupported game. PlaceId=%s GameId=%s"):format(tostring(game.PlaceId), tostring(game.GameId))
    end

    status.Text = "Downloading script..."
    for attempt = 1, 3 do
        local source = fetch(url)
        if source then return source end
        task.wait(0.5)
    end

    return nil, "Could not download the script. Check your connection or executor."
end

-- [LOADER] The main thread waits for the key UI, then fetches and compiles the
--  payload. The payload itself runs in task.spawn so the Continue button and
--  the rest of the game thread are not blocked.
local function runLaunch()
    while true do
        while not launchRequest do
            task.wait(0.1)
        end

        local key = launchRequest
        launchRequest = nil

        status.Text = "Loading Synvextia..."
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Loading"

        local started = os.clock()
        local okCall, payload, err = pcall(deliver, key)
        if not okCall then
            payload, err = nil, tostring(payload)
        end

        if not payload then
            -- keep the UI alive so the key can be retried
            accepted = false
            status.Text = tostring(err or "Loader error")
            status.TextColor3 = COL_ERROR
            checkButton.Text = "Check Key"
            warn("[Synvextia] " .. tostring(err))
        else
            print(("[Synvextia] payload: %d bytes in %.1fs"):format(#payload, os.clock() - started))

            local chunk, compileErr = loadstring(payload)
            if not chunk then
                accepted = false
                status.Text = "Loader script failed to compile"
                status.TextColor3 = COL_ERROR
                checkButton.Text = "Check Key"
                warn("[Synvextia] compile error: " .. tostring(compileErr))
            else
                pcall(function() screenGui:Destroy() end)

                -- Let the pulse loop and any click/auto-login thread finish
                -- before spawning the payload thread.
                task.wait(0.3)

                task.spawn(function()
                    local okRun, runErr = pcall(chunk)
                    if okRun then
                        print(("[Synvextia] loader returned after %.1fs"):format(os.clock() - started))
                    else
                        warn(("[Synvextia] loader failed after %.1fs: %s"):format(os.clock() - started, tostring(runErr)))
                    end
                end)
                break
            end
        end
    end
end

local function checkKey(isAuto)
    if accepted then return end
    local key = normalizeKey(keyBox.Text)
    if key == "" then
        if not isAuto then
            status.Text = "Enter a key first"
            status.TextColor3 = COL_ERROR
        end
        return
    end
    -- [NOTE] Local key check.
    if VALID_KEYS[key] then
        accepted = true
        saveKey(key)
        status.Text = isAuto and "Saved key found! Logging in..." or "Key accepted!"
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Success"
        task.wait(0.6)
        launchRequest = key
    else
        status.Text = "Invalid key - join the server for one"
        status.TextColor3 = COL_ERROR
        if isAuto then
            clearSavedKey()
            keyBox.Text = ""
        end
    end
end

joinButton.MouseButton1Click:Connect(function()
    if busy then return end
    busy = true
    local copied = false
    local fns = {}
    if typeof(setclipboard) == "function" then table.insert(fns, setclipboard) end
    if typeof(writeclipboard) == "function" then table.insert(fns, writeclipboard) end
    table.insert(fns, function(t) return GuiService:SetClipboard(t) end)

    for _, fn in ipairs(fns) do
        local ok = pcall(fn, INVITE)
        if ok then copied = true break end
    end
    if not copied then
        keyBox.Text = INVITE
    end
    joinButton.Text = copied and "Copied! Paste in Discord" or "Invite in box - copy it"
    task.wait(1.8)
    joinButton.Text = "Copy Discord Invite"
    busy = false
end)

checkButton.MouseButton1Click:Connect(function() checkKey(false) end)
keyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then checkKey(false) end
end)

local lastAuto = 0
keyBox:GetPropertyChangedSignal("Text"):Connect(function()
    if accepted then return end
    local k = normalizeKey(keyBox.Text)
    if VALID_KEYS[k] and tick() - lastAuto > 1 then
        lastAuto = tick()
        checkKey(false)
    end
end)

task.spawn(function()
    local saved = loadSavedKey()
    if saved ~= "" then
        keyBox.Text = saved
        status.Text = "Saved key found! Logging in..."
        status.TextColor3 = COL_SUBTEXT
        task.wait(0.6)
        if not screenGui.Parent then return end
        checkKey(true)
    end
end)

task.spawn(function()
    while screenGui.Parent do
        local pulse = math.sin(tick() * 2) * 0.5 + 0.5
        joinGradient.Offset = Vector2.new(0, pulse * 0.6 - 0.3)
        RunService.RenderStepped:Wait()
    end
end)

-- The main thread waits for the key UI, then fetches and compiles the payload.
-- The payload runs in task.spawn so it does not block the UI or game thread.
runLaunch()



-- [HTTPGET #7]: https://raw.githubusercontent.com/SynvextiaHub/Loader./main/SYN
--[[
  Synvextia Key System -> per-game loader
  Key: syn2
  Preserves request-first fetch and task.spawn execution.
]]

print("[Synvextia] loader v2 (direct per-game URLs)")

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local GuiService = game:GetService("GuiService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local INVITE = "https://discord.gg/6YQagDhEqy"
local MESSAGE = "Join the server to get your key\nThere is no checkpoints"
local VALID_KEYS = {
    ["syn2"] = true,
}

local KEY_FILE = "synvextia_key.txt"

local function normalizeKey(s)
    return tostring(s or ""):gsub("%s+", "")
end

-- [NOTE] Some builds read getgenv().SCRIPT_KEY; set both names for compatibility.
local function saveKey(key)
    key = normalizeKey(key)
    if key == "" then return end
    pcall(function()
        if writefile then writefile(KEY_FILE, key) end
    end)
    pcall(function()
        getgenv().SCRIPT_KEY = key
        getgenv().SynvextiaKey = key
    end)
    pcall(function()
        _G.SCRIPT_KEY = key
        _G.SynvextiaKey = key
    end)
end

local function loadSavedKey()
    if typeof(isfile) == "function" and typeof(readfile) == "function" then
        local ok, is = pcall(function() return isfile(KEY_FILE) end)
        if ok and is then
            local ok2, contents = pcall(function() return readfile(KEY_FILE) end)
            if ok2 and contents then
                local k = normalizeKey(contents)
                if k ~= "" then return k end
            end
        end
    end
    if typeof(getgenv) == "function" then
        local ok, k = pcall(function() return getgenv().SCRIPT_KEY or getgenv().SynvextiaKey end)
        if ok and k and normalizeKey(k) ~= "" then return normalizeKey(k) end
    end
    if _G.SynvextiaKey and normalizeKey(_G.SynvextiaKey) ~= "" then
        return normalizeKey(_G.SynvextiaKey)
    end
    return ""
end

local function clearSavedKey()
    pcall(function()
        if typeof(delfile) == "function" and typeof(isfile) == "function" then
            if isfile(KEY_FILE) then delfile(KEY_FILE) end
        elseif writefile then
            writefile(KEY_FILE, "")
        end
    end)
    pcall(function() getgenv().SCRIPT_KEY = nil end)
    pcall(function() _G.SynvextiaKey = nil end)
end

local COL_BG_TOP = Color3.fromRGB(24, 25, 32)
local COL_BG_BOTTOM = Color3.fromRGB(12, 12, 17)
local COL_PANEL_TOP = Color3.fromRGB(48, 50, 58)
local COL_PANEL_BOTTOM = Color3.fromRGB(34, 36, 42)
local COL_ACCENT = Color3.fromRGB(88, 101, 242)
local COL_ACCENT_HOVER = Color3.fromRGB(108, 120, 255)
local COL_SUCCESS = Color3.fromRGB(35, 134, 78)
local COL_ERROR = Color3.fromRGB(178, 58, 72)
local COL_TEXT = Color3.fromRGB(245, 246, 250)
local COL_SUBTEXT = Color3.fromRGB(160, 165, 185)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "SynvextiaKeySystem"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 9999
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

local overlay = Instance.new("Frame")
overlay.Name = "Overlay"
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = COL_BG_BOTTOM
overlay.BackgroundTransparency = 1
overlay.BorderSizePixel = 0
overlay.ZIndex = 1
overlay.Parent = screenGui

local backdropGradient = Instance.new("UIGradient")
backdropGradient.Color = ColorSequence.new(COL_BG_TOP, COL_BG_BOTTOM)
backdropGradient.Rotation = 45
backdropGradient.Parent = overlay
TweenService:Create(overlay, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), { BackgroundTransparency = 0.25 }):Play()

local panel = Instance.new("Frame")
panel.Name = "Panel"
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Position = UDim2.fromScale(0.5, 0.5)
panel.Size = UDim2.new(0.9, 0, 0, 420)
panel.BackgroundColor3 = COL_PANEL_BOTTOM
panel.BorderSizePixel = 0
panel.ZIndex = 2
panel.Parent = overlay

local panelSize = Instance.new("UISizeConstraint")
panelSize.MaxSize = Vector2.new(660, 420)
panelSize.MinSize = Vector2.new(300, 420)
panelSize.Parent = panel

local panelGradient = Instance.new("UIGradient")
panelGradient.Color = ColorSequence.new(COL_PANEL_TOP, COL_PANEL_BOTTOM)
panelGradient.Rotation = 90
panelGradient.Parent = panel

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 18)
panelCorner.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Color = Color3.fromRGB(255, 255, 255)
panelStroke.Transparency = 0.85
panelStroke.Thickness = 1.5
panelStroke.Parent = panel

local accent = Instance.new("Frame")
accent.Name = "Accent"
accent.Size = UDim2.new(1, -80, 0, 6)
accent.Position = UDim2.new(0.5, 0, 0, 24)
accent.AnchorPoint = Vector2.new(0.5, 0)
accent.BackgroundColor3 = COL_ACCENT
accent.BorderSizePixel = 0
accent.ZIndex = 3
accent.Parent = panel
Instance.new("UICorner", accent).CornerRadius = UDim.new(1, 0)

local accentGradient = Instance.new("UIGradient")
accentGradient.Color = ColorSequence.new(Color3.fromRGB(120, 130, 255), COL_ACCENT)
accentGradient.Parent = accent

local wordmark = Instance.new("TextLabel")
wordmark.Name = "Wordmark"
wordmark.AnchorPoint = Vector2.new(0.5, 0)
wordmark.Position = UDim2.new(0.5, 0, 0, 44)
wordmark.Size = UDim2.new(1, -40, 0, 18)
wordmark.BackgroundTransparency = 1
wordmark.Text = "S Y N V E X T I A"
wordmark.TextColor3 = COL_ACCENT_HOVER
wordmark.TextSize = 14
wordmark.Font = Enum.Font.GothamBold
wordmark.TextTransparency = 0.25
wordmark.ZIndex = 3
wordmark.Parent = panel

local title = Instance.new("TextLabel")
title.Name = "Title"
title.AnchorPoint = Vector2.new(0.5, 0)
title.Position = UDim2.new(0.5, 0, 0, 70)
title.Size = UDim2.new(1, -50, 0, 40)
title.BackgroundTransparency = 1
title.Text = "Key System"
title.TextColor3 = COL_TEXT
title.TextSize = 30
title.Font = Enum.Font.GothamBold
title.ZIndex = 3
title.Parent = panel

local message = Instance.new("TextLabel")
message.Name = "Message"
message.AnchorPoint = Vector2.new(0.5, 0)
message.Position = UDim2.new(0.5, 0, 0, 108)
message.Size = UDim2.new(1, -50, 0, 52)
message.BackgroundTransparency = 1
message.Text = MESSAGE
message.TextColor3 = COL_SUBTEXT
message.TextWrapped = true
message.TextSize = 16
message.Font = Enum.Font.Gotham
message.TextXAlignment = Enum.TextXAlignment.Center
message.ZIndex = 3
message.Parent = panel

local joinButton = Instance.new("TextButton")
joinButton.Name = "JoinButton"
joinButton.AnchorPoint = Vector2.new(0.5, 0)
joinButton.Position = UDim2.new(0.5, 0, 0, 164)
joinButton.Size = UDim2.new(1, -100, 0, 50)
joinButton.BackgroundColor3 = COL_ACCENT
joinButton.BorderSizePixel = 0
joinButton.Text = "Copy Discord Invite"
joinButton.TextColor3 = Color3.new(1, 1, 1)
joinButton.TextSize = 22
joinButton.Font = Enum.Font.GothamBold
joinButton.AutoButtonColor = false
joinButton.ZIndex = 3
joinButton.Parent = panel
Instance.new("UICorner", joinButton).CornerRadius = UDim.new(0, 14)

local joinGradient = Instance.new("UIGradient")
joinGradient.Color = ColorSequence.new(COL_ACCENT_HOVER, COL_ACCENT)
joinGradient.Rotation = 90
joinGradient.Parent = joinButton

local joinScale = Instance.new("UIScale")
joinScale.Parent = joinButton
joinButton.MouseEnter:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
joinButton.MouseLeave:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local keyBox = Instance.new("TextBox")
keyBox.Name = "KeyBox"
keyBox.AnchorPoint = Vector2.new(0.5, 0)
keyBox.Position = UDim2.new(0.5, 0, 0, 236)
keyBox.Size = UDim2.new(1, -110, 0, 42)
keyBox.BackgroundColor3 = Color3.fromRGB(20, 21, 26)
keyBox.BackgroundTransparency = 0.25
keyBox.BorderSizePixel = 0
keyBox.ClearTextOnFocus = false
keyBox.Font = Enum.Font.Code
keyBox.PlaceholderText = "Paste your key here..."
keyBox.Text = ""
keyBox.TextColor3 = COL_TEXT
keyBox.PlaceholderColor3 = COL_SUBTEXT
keyBox.TextSize = 16
keyBox.TextXAlignment = Enum.TextXAlignment.Center
keyBox.ZIndex = 3
keyBox.Parent = panel
Instance.new("UICorner", keyBox).CornerRadius = UDim.new(0, 8)

local checkButton = Instance.new("TextButton")
checkButton.Name = "CheckButton"
checkButton.AnchorPoint = Vector2.new(0.5, 0)
checkButton.Position = UDim2.new(0.5, 0, 0, 296)
checkButton.Size = UDim2.new(1, -100, 0, 50)
checkButton.BackgroundColor3 = COL_SUCCESS
checkButton.BorderSizePixel = 0
checkButton.Text = "Check Key"
checkButton.TextColor3 = Color3.new(1, 1, 1)
checkButton.TextSize = 22
checkButton.Font = Enum.Font.GothamBold
checkButton.AutoButtonColor = false
checkButton.ZIndex = 3
checkButton.Parent = panel
Instance.new("UICorner", checkButton).CornerRadius = UDim.new(0, 14)

local checkScale = Instance.new("UIScale")
checkScale.Parent = checkButton
checkButton.MouseEnter:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
checkButton.MouseLeave:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local status = Instance.new("TextLabel")
status.Name = "Status"
status.AnchorPoint = Vector2.new(0.5, 0)
status.Position = UDim2.new(0.5, 0, 0, 360)
status.Size = UDim2.new(1, -40, 0, 20)
status.BackgroundTransparency = 1
status.Text = ""
status.TextColor3 = COL_SUBTEXT
status.TextSize = 14
status.Font = Enum.Font.Gotham
status.ZIndex = 3
status.Parent = panel

local busy = false
local accepted = false
local launchRequest = nil

-- [LOADER] Request-first fetch, then game:HttpGet fallback.
local function fetch(url)
    local req = (type(syn) == "table" and syn.request) or request or http_request
    if type(req) == "function" then
        local ok, res = pcall(req, { Url = url, Method = "GET" })
        if ok and type(res) == "table" and tonumber(res.StatusCode) == 200 and type(res.Body) == "string" and res.Body ~= "" then
            return res.Body
        end
    end

    local ok, source = pcall(game.HttpGet, game, url)
    if ok and type(source) == "string" and source ~= "" then
        return source
    end

    return nil
end

local SCRIPTS = {
    MM2        = "https://api.jnkie.com/api/v1/luascripts/public/f88bc27f071600baaa1afc246ffb6c53461c215a7db93c969959072152943cd5/download",
    DOORS      = "https://api.jnkie.com/api/v1/luascripts/public/7915991c0c868d1938aff55d370c8050e063cbcb8762a95fd405f21b8587ea2c/download",
    TIMEBOMB   = "https://api.jnkie.com/api/v1/luascripts/public/69a06a1de9966f3012fb2bd2cb8d5d2af674dc9125f4d0ba7b4fd323a8dce635/download",
    FORSAKEN   = "https://api.jnkie.com/api/v1/luascripts/public/7c4032d89f36d9fab5ac0076a4802086eebc9d17c223283ea042bc9753ebd2cc/download",
    DEADRAILS  = "https://api.jnkie.com/api/v1/luascripts/public/19ab1970bbdf3b967d63349f52d7967b0e7a39860a4e463f2f4771a165aa543e/download",
    VOLLEYBALL = "https://api.jnkie.com/api/v1/luascripts/public/41bf8158fc125b3d895f332771b5aeaed072c5b8ea16d8002d0878644fa3578f/download",
    NIGHTS99   = "https://api.jnkie.com/api/v1/luascripts/public/1238dbd70c6f460836b85fca2e3311debed55047f9e21b8207de07caf7867d0f/download",
    HUSSVALLEY = "https://api.jnkie.com/api/v1/luascripts/public/fafaa6d66f82d1f8448f07b70e342014c18adc491dda695c13c0547776342f7e/download",
}

local byGameId = {
    [6931042565] = SCRIPTS.VOLLEYBALL,
    [2440500124] = SCRIPTS.DOORS,
}

local byPlaceId = {
    -- Murder Mystery 2
    [142823291] = SCRIPTS.MM2,
    [335132309] = SCRIPTS.MM2,
    [636649648] = SCRIPTS.MM2,
    [80469437126309] = SCRIPTS.MM2,

    -- DOORS
    [6516141723] = SCRIPTS.DOORS,
    [6839171747] = SCRIPTS.DOORS,
    [10549820578] = SCRIPTS.DOORS,
    [12308344607] = SCRIPTS.DOORS,
    [87716067947993] = SCRIPTS.DOORS,
    [110258689672367] = SCRIPTS.DOORS,

    -- Timebomb Duels
    [11379739543] = SCRIPTS.TIMEBOMB,

    -- Forsaken
    [18687417158] = SCRIPTS.FORSAKEN,
    [83645629621104] = SCRIPTS.FORSAKEN,
    [86454545238517] = SCRIPTS.FORSAKEN,
    [94626476208514] = SCRIPTS.FORSAKEN,
    [106560117662077] = SCRIPTS.FORSAKEN,

    -- Dead Rails
    [70876832253163] = SCRIPTS.DEADRAILS,
    [74106709399219] = SCRIPTS.DEADRAILS,
    [96831577561553] = SCRIPTS.DEADRAILS,
    [110282088381749] = SCRIPTS.DEADRAILS,
    [111285651581407] = SCRIPTS.DEADRAILS,
    [116495829188952] = SCRIPTS.DEADRAILS,

    -- Volleyball Legends
    [73956553001240] = SCRIPTS.VOLLEYBALL,
    [74691681039273] = SCRIPTS.VOLLEYBALL,
    [85395484560711] = SCRIPTS.VOLLEYBALL,
    [86789627188240] = SCRIPTS.VOLLEYBALL,
    [96802054849934] = SCRIPTS.VOLLEYBALL,
    [102580589030177] = SCRIPTS.VOLLEYBALL,
    [103521881639626] = SCRIPTS.VOLLEYBALL,
    [109684591839194] = SCRIPTS.VOLLEYBALL,
    [117134837736236] = SCRIPTS.VOLLEYBALL,
    [134314141048307] = SCRIPTS.VOLLEYBALL,

    -- 99 Nights in the Forest
    [79546208627805] = SCRIPTS.NIGHTS99,
    [126509999114328] = SCRIPTS.NIGHTS99,

    -- Huss Valley
    [107535308163741] = SCRIPTS.HUSSVALLEY,
}

local function getScriptUrl()
    local gameId = game.GameId
    while gameId == 0 and game.PlaceId == 0 do
        task.wait()
        gameId = game.GameId
    end
    return byGameId[gameId] or byPlaceId[game.PlaceId]
end

-- Returns the payload source, or nil plus a message for the UI.
local function deliver(key)
    local url = getScriptUrl()
    if not url then
        return nil, ("Unsupported game. PlaceId=%s GameId=%s"):format(tostring(game.PlaceId), tostring(game.GameId))
    end

    status.Text = "Downloading script..."
    for attempt = 1, 3 do
        local source = fetch(url)
        if source then return source end
        task.wait(0.5)
    end

    return nil, "Could not download the script. Check your connection or executor."
end

-- [LOADER] The main thread waits for the key UI, then fetches and compiles the
--  payload. The payload itself runs in task.spawn so the Continue button and
--  the rest of the game thread are not blocked.
local function runLaunch()
    while true do
        while not launchRequest do
            task.wait(0.1)
        end

        local key = launchRequest
        launchRequest = nil

        status.Text = "Loading Synvextia..."
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Loading"

        local started = os.clock()
        local okCall, payload, err = pcall(deliver, key)
        if not okCall then
            payload, err = nil, tostring(payload)
        end

        if not payload then
            -- keep the UI alive so the key can be retried
            accepted = false
            status.Text = tostring(err or "Loader error")
            status.TextColor3 = COL_ERROR
            checkButton.Text = "Check Key"
            warn("[Synvextia] " .. tostring(err))
        else
            print(("[Synvextia] payload: %d bytes in %.1fs"):format(#payload, os.clock() - started))

            local chunk, compileErr = loadstring(payload)
            if not chunk then
                accepted = false
                status.Text = "Loader script failed to compile"
                status.TextColor3 = COL_ERROR
                checkButton.Text = "Check Key"
                warn("[Synvextia] compile error: " .. tostring(compileErr))
            else
                pcall(function() screenGui:Destroy() end)

                -- Let the pulse loop and any click/auto-login thread finish
                -- before spawning the payload thread.
                task.wait(0.3)

                task.spawn(function()
                    local okRun, runErr = pcall(chunk)
                    if okRun then
                        print(("[Synvextia] loader returned after %.1fs"):format(os.clock() - started))
                    else
                        warn(("[Synvextia] loader failed after %.1fs: %s"):format(os.clock() - started, tostring(runErr)))
                    end
                end)
                break
            end
        end
    end
end

local function checkKey(isAuto)
    if accepted then return end
    local key = normalizeKey(keyBox.Text)
    if key == "" then
        if not isAuto then
            status.Text = "Enter a key first"
            status.TextColor3 = COL_ERROR
        end
        return
    end
    -- [NOTE] Local key check.
    if VALID_KEYS[key] then
        accepted = true
        saveKey(key)
        status.Text = isAuto and "Saved key found! Logging in..." or "Key accepted!"
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Success"
        task.wait(0.6)
        launchRequest = key
    else
        status.Text = "Invalid key - join the server for one"
        status.TextColor3 = COL_ERROR
        if isAuto then
            clearSavedKey()
            keyBox.Text = ""
        end
    end
end

joinButton.MouseButton1Click:Connect(function()
    if busy then return end
    busy = true
    local copied = false
    local fns = {}
    if typeof(setclipboard) == "function" then table.insert(fns, setclipboard) end
    if typeof(writeclipboard) == "function" then table.insert(fns, writeclipboard) end
    table.insert(fns, function(t) return GuiService:SetClipboard(t) end)

    for _, fn in ipairs(fns) do
        local ok = pcall(fn, INVITE)
        if ok then copied = true break end
    end
    if not copied then
        keyBox.Text = INVITE
    end
    joinButton.Text = copied and "Copied! Paste in Discord" or "Invite in box - copy it"
    task.wait(1.8)
    joinButton.Text = "Copy Discord Invite"
    busy = false
end)

checkButton.MouseButton1Click:Connect(function() checkKey(false) end)
keyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then checkKey(false) end
end)

local lastAuto = 0
keyBox:GetPropertyChangedSignal("Text"):Connect(function()
    if accepted then return end
    local k = normalizeKey(keyBox.Text)
    if VALID_KEYS[k] and tick() - lastAuto > 1 then
        lastAuto = tick()
        checkKey(false)
    end
end)

task.spawn(function()
    local saved = loadSavedKey()
    if saved ~= "" then
        keyBox.Text = saved
        status.Text = "Saved key found! Logging in..."
        status.TextColor3 = COL_SUBTEXT
        task.wait(0.6)
        if not screenGui.Parent then return end
        checkKey(true)
    end
end)

task.spawn(function()
    while screenGui.Parent do
        local pulse = math.sin(tick() * 2) * 0.5 + 0.5
        joinGradient.Offset = Vector2.new(0, pulse * 0.6 - 0.3)
        RunService.RenderStepped:Wait()
    end
end)

-- The main thread waits for the key UI, then fetches and compiles the payload.
-- The payload runs in task.spawn so it does not block the UI or game thread.
runLaunch()



-- [LOADSTRING #8] - Chunk: nil
--[[
  Synvextia Key System -> per-game loader
  Key: syn2
  Preserves request-first fetch and task.spawn execution.
]]

print("[Synvextia] loader v2 (direct per-game URLs)")

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local GuiService = game:GetService("GuiService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local INVITE = "https://discord.gg/6YQagDhEqy"
local MESSAGE = "Join the server to get your key\nThere is no checkpoints"
local VALID_KEYS = {
    ["syn2"] = true,
}

local KEY_FILE = "synvextia_key.txt"

local function normalizeKey(s)
    return tostring(s or ""):gsub("%s+", "")
end

-- [NOTE] Some builds read getgenv().SCRIPT_KEY; set both names for compatibility.
local function saveKey(key)
    key = normalizeKey(key)
    if key == "" then return end
    pcall(function()
        if writefile then writefile(KEY_FILE, key) end
    end)
    pcall(function()
        getgenv().SCRIPT_KEY = key
        getgenv().SynvextiaKey = key
    end)
    pcall(function()
        _G.SCRIPT_KEY = key
        _G.SynvextiaKey = key
    end)
end

local function loadSavedKey()
    if typeof(isfile) == "function" and typeof(readfile) == "function" then
        local ok, is = pcall(function() return isfile(KEY_FILE) end)
        if ok and is then
            local ok2, contents = pcall(function() return readfile(KEY_FILE) end)
            if ok2 and contents then
                local k = normalizeKey(contents)
                if k ~= "" then return k end
            end
        end
    end
    if typeof(getgenv) == "function" then
        local ok, k = pcall(function() return getgenv().SCRIPT_KEY or getgenv().SynvextiaKey end)
        if ok and k and normalizeKey(k) ~= "" then return normalizeKey(k) end
    end
    if _G.SynvextiaKey and normalizeKey(_G.SynvextiaKey) ~= "" then
        return normalizeKey(_G.SynvextiaKey)
    end
    return ""
end

local function clearSavedKey()
    pcall(function()
        if typeof(delfile) == "function" and typeof(isfile) == "function" then
            if isfile(KEY_FILE) then delfile(KEY_FILE) end
        elseif writefile then
            writefile(KEY_FILE, "")
        end
    end)
    pcall(function() getgenv().SCRIPT_KEY = nil end)
    pcall(function() _G.SynvextiaKey = nil end)
end

local COL_BG_TOP = Color3.fromRGB(24, 25, 32)
local COL_BG_BOTTOM = Color3.fromRGB(12, 12, 17)
local COL_PANEL_TOP = Color3.fromRGB(48, 50, 58)
local COL_PANEL_BOTTOM = Color3.fromRGB(34, 36, 42)
local COL_ACCENT = Color3.fromRGB(88, 101, 242)
local COL_ACCENT_HOVER = Color3.fromRGB(108, 120, 255)
local COL_SUCCESS = Color3.fromRGB(35, 134, 78)
local COL_ERROR = Color3.fromRGB(178, 58, 72)
local COL_TEXT = Color3.fromRGB(245, 246, 250)
local COL_SUBTEXT = Color3.fromRGB(160, 165, 185)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "SynvextiaKeySystem"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 9999
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

local overlay = Instance.new("Frame")
overlay.Name = "Overlay"
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = COL_BG_BOTTOM
overlay.BackgroundTransparency = 1
overlay.BorderSizePixel = 0
overlay.ZIndex = 1
overlay.Parent = screenGui

local backdropGradient = Instance.new("UIGradient")
backdropGradient.Color = ColorSequence.new(COL_BG_TOP, COL_BG_BOTTOM)
backdropGradient.Rotation = 45
backdropGradient.Parent = overlay
TweenService:Create(overlay, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), { BackgroundTransparency = 0.25 }):Play()

local panel = Instance.new("Frame")
panel.Name = "Panel"
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Position = UDim2.fromScale(0.5, 0.5)
panel.Size = UDim2.new(0.9, 0, 0, 420)
panel.BackgroundColor3 = COL_PANEL_BOTTOM
panel.BorderSizePixel = 0
panel.ZIndex = 2
panel.Parent = overlay

local panelSize = Instance.new("UISizeConstraint")
panelSize.MaxSize = Vector2.new(660, 420)
panelSize.MinSize = Vector2.new(300, 420)
panelSize.Parent = panel

local panelGradient = Instance.new("UIGradient")
panelGradient.Color = ColorSequence.new(COL_PANEL_TOP, COL_PANEL_BOTTOM)
panelGradient.Rotation = 90
panelGradient.Parent = panel

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 18)
panelCorner.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Color = Color3.fromRGB(255, 255, 255)
panelStroke.Transparency = 0.85
panelStroke.Thickness = 1.5
panelStroke.Parent = panel

local accent = Instance.new("Frame")
accent.Name = "Accent"
accent.Size = UDim2.new(1, -80, 0, 6)
accent.Position = UDim2.new(0.5, 0, 0, 24)
accent.AnchorPoint = Vector2.new(0.5, 0)
accent.BackgroundColor3 = COL_ACCENT
accent.BorderSizePixel = 0
accent.ZIndex = 3
accent.Parent = panel
Instance.new("UICorner", accent).CornerRadius = UDim.new(1, 0)

local accentGradient = Instance.new("UIGradient")
accentGradient.Color = ColorSequence.new(Color3.fromRGB(120, 130, 255), COL_ACCENT)
accentGradient.Parent = accent

local wordmark = Instance.new("TextLabel")
wordmark.Name = "Wordmark"
wordmark.AnchorPoint = Vector2.new(0.5, 0)
wordmark.Position = UDim2.new(0.5, 0, 0, 44)
wordmark.Size = UDim2.new(1, -40, 0, 18)
wordmark.BackgroundTransparency = 1
wordmark.Text = "S Y N V E X T I A"
wordmark.TextColor3 = COL_ACCENT_HOVER
wordmark.TextSize = 14
wordmark.Font = Enum.Font.GothamBold
wordmark.TextTransparency = 0.25
wordmark.ZIndex = 3
wordmark.Parent = panel

local title = Instance.new("TextLabel")
title.Name = "Title"
title.AnchorPoint = Vector2.new(0.5, 0)
title.Position = UDim2.new(0.5, 0, 0, 70)
title.Size = UDim2.new(1, -50, 0, 40)
title.BackgroundTransparency = 1
title.Text = "Key System"
title.TextColor3 = COL_TEXT
title.TextSize = 30
title.Font = Enum.Font.GothamBold
title.ZIndex = 3
title.Parent = panel

local message = Instance.new("TextLabel")
message.Name = "Message"
message.AnchorPoint = Vector2.new(0.5, 0)
message.Position = UDim2.new(0.5, 0, 0, 108)
message.Size = UDim2.new(1, -50, 0, 52)
message.BackgroundTransparency = 1
message.Text = MESSAGE
message.TextColor3 = COL_SUBTEXT
message.TextWrapped = true
message.TextSize = 16
message.Font = Enum.Font.Gotham
message.TextXAlignment = Enum.TextXAlignment.Center
message.ZIndex = 3
message.Parent = panel

local joinButton = Instance.new("TextButton")
joinButton.Name = "JoinButton"
joinButton.AnchorPoint = Vector2.new(0.5, 0)
joinButton.Position = UDim2.new(0.5, 0, 0, 164)
joinButton.Size = UDim2.new(1, -100, 0, 50)
joinButton.BackgroundColor3 = COL_ACCENT
joinButton.BorderSizePixel = 0
joinButton.Text = "Copy Discord Invite"
joinButton.TextColor3 = Color3.new(1, 1, 1)
joinButton.TextSize = 22
joinButton.Font = Enum.Font.GothamBold
joinButton.AutoButtonColor = false
joinButton.ZIndex = 3
joinButton.Parent = panel
Instance.new("UICorner", joinButton).CornerRadius = UDim.new(0, 14)

local joinGradient = Instance.new("UIGradient")
joinGradient.Color = ColorSequence.new(COL_ACCENT_HOVER, COL_ACCENT)
joinGradient.Rotation = 90
joinGradient.Parent = joinButton

local joinScale = Instance.new("UIScale")
joinScale.Parent = joinButton
joinButton.MouseEnter:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
joinButton.MouseLeave:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local keyBox = Instance.new("TextBox")
keyBox.Name = "KeyBox"
keyBox.AnchorPoint = Vector2.new(0.5, 0)
keyBox.Position = UDim2.new(0.5, 0, 0, 236)
keyBox.Size = UDim2.new(1, -110, 0, 42)
keyBox.BackgroundColor3 = Color3.fromRGB(20, 21, 26)
keyBox.BackgroundTransparency = 0.25
keyBox.BorderSizePixel = 0
keyBox.ClearTextOnFocus = false
keyBox.Font = Enum.Font.Code
keyBox.PlaceholderText = "Paste your key here..."
keyBox.Text = ""
keyBox.TextColor3 = COL_TEXT
keyBox.PlaceholderColor3 = COL_SUBTEXT
keyBox.TextSize = 16
keyBox.TextXAlignment = Enum.TextXAlignment.Center
keyBox.ZIndex = 3
keyBox.Parent = panel
Instance.new("UICorner", keyBox).CornerRadius = UDim.new(0, 8)

local checkButton = Instance.new("TextButton")
checkButton.Name = "CheckButton"
checkButton.AnchorPoint = Vector2.new(0.5, 0)
checkButton.Position = UDim2.new(0.5, 0, 0, 296)
checkButton.Size = UDim2.new(1, -100, 0, 50)
checkButton.BackgroundColor3 = COL_SUCCESS
checkButton.BorderSizePixel = 0
checkButton.Text = "Check Key"
checkButton.TextColor3 = Color3.new(1, 1, 1)
checkButton.TextSize = 22
checkButton.Font = Enum.Font.GothamBold
checkButton.AutoButtonColor = false
checkButton.ZIndex = 3
checkButton.Parent = panel
Instance.new("UICorner", checkButton).CornerRadius = UDim.new(0, 14)

local checkScale = Instance.new("UIScale")
checkScale.Parent = checkButton
checkButton.MouseEnter:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
checkButton.MouseLeave:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local status = Instance.new("TextLabel")
status.Name = "Status"
status.AnchorPoint = Vector2.new(0.5, 0)
status.Position = UDim2.new(0.5, 0, 0, 360)
status.Size = UDim2.new(1, -40, 0, 20)
status.BackgroundTransparency = 1
status.Text = ""
status.TextColor3 = COL_SUBTEXT
status.TextSize = 14
status.Font = Enum.Font.Gotham
status.ZIndex = 3
status.Parent = panel

local busy = false
local accepted = false
local launchRequest = nil

-- [LOADER] Request-first fetch, then game:HttpGet fallback.
local function fetch(url)
    local req = (type(syn) == "table" and syn.request) or request or http_request
    if type(req) == "function" then
        local ok, res = pcall(req, { Url = url, Method = "GET" })
        if ok and type(res) == "table" and tonumber(res.StatusCode) == 200 and type(res.Body) == "string" and res.Body ~= "" then
            return res.Body
        end
    end

    local ok, source = pcall(game.HttpGet, game, url)
    if ok and type(source) == "string" and source ~= "" then
        return source
    end

    return nil
end

local SCRIPTS = {
    MM2        = "https://api.jnkie.com/api/v1/luascripts/public/f88bc27f071600baaa1afc246ffb6c53461c215a7db93c969959072152943cd5/download",
    DOORS      = "https://api.jnkie.com/api/v1/luascripts/public/7915991c0c868d1938aff55d370c8050e063cbcb8762a95fd405f21b8587ea2c/download",
    TIMEBOMB   = "https://api.jnkie.com/api/v1/luascripts/public/69a06a1de9966f3012fb2bd2cb8d5d2af674dc9125f4d0ba7b4fd323a8dce635/download",
    FORSAKEN   = "https://api.jnkie.com/api/v1/luascripts/public/7c4032d89f36d9fab5ac0076a4802086eebc9d17c223283ea042bc9753ebd2cc/download",
    DEADRAILS  = "https://api.jnkie.com/api/v1/luascripts/public/19ab1970bbdf3b967d63349f52d7967b0e7a39860a4e463f2f4771a165aa543e/download",
    VOLLEYBALL = "https://api.jnkie.com/api/v1/luascripts/public/41bf8158fc125b3d895f332771b5aeaed072c5b8ea16d8002d0878644fa3578f/download",
    NIGHTS99   = "https://api.jnkie.com/api/v1/luascripts/public/1238dbd70c6f460836b85fca2e3311debed55047f9e21b8207de07caf7867d0f/download",
    HUSSVALLEY = "https://api.jnkie.com/api/v1/luascripts/public/fafaa6d66f82d1f8448f07b70e342014c18adc491dda695c13c0547776342f7e/download",
}

local byGameId = {
    [6931042565] = SCRIPTS.VOLLEYBALL,
    [2440500124] = SCRIPTS.DOORS,
}

local byPlaceId = {
    -- Murder Mystery 2
    [142823291] = SCRIPTS.MM2,
    [335132309] = SCRIPTS.MM2,
    [636649648] = SCRIPTS.MM2,
    [80469437126309] = SCRIPTS.MM2,

    -- DOORS
    [6516141723] = SCRIPTS.DOORS,
    [6839171747] = SCRIPTS.DOORS,
    [10549820578] = SCRIPTS.DOORS,
    [12308344607] = SCRIPTS.DOORS,
    [87716067947993] = SCRIPTS.DOORS,
    [110258689672367] = SCRIPTS.DOORS,

    -- Timebomb Duels
    [11379739543] = SCRIPTS.TIMEBOMB,

    -- Forsaken
    [18687417158] = SCRIPTS.FORSAKEN,
    [83645629621104] = SCRIPTS.FORSAKEN,
    [86454545238517] = SCRIPTS.FORSAKEN,
    [94626476208514] = SCRIPTS.FORSAKEN,
    [106560117662077] = SCRIPTS.FORSAKEN,

    -- Dead Rails
    [70876832253163] = SCRIPTS.DEADRAILS,
    [74106709399219] = SCRIPTS.DEADRAILS,
    [96831577561553] = SCRIPTS.DEADRAILS,
    [110282088381749] = SCRIPTS.DEADRAILS,
    [111285651581407] = SCRIPTS.DEADRAILS,
    [116495829188952] = SCRIPTS.DEADRAILS,

    -- Volleyball Legends
    [73956553001240] = SCRIPTS.VOLLEYBALL,
    [74691681039273] = SCRIPTS.VOLLEYBALL,
    [85395484560711] = SCRIPTS.VOLLEYBALL,
    [86789627188240] = SCRIPTS.VOLLEYBALL,
    [96802054849934] = SCRIPTS.VOLLEYBALL,
    [102580589030177] = SCRIPTS.VOLLEYBALL,
    [103521881639626] = SCRIPTS.VOLLEYBALL,
    [109684591839194] = SCRIPTS.VOLLEYBALL,
    [117134837736236] = SCRIPTS.VOLLEYBALL,
    [134314141048307] = SCRIPTS.VOLLEYBALL,

    -- 99 Nights in the Forest
    [79546208627805] = SCRIPTS.NIGHTS99,
    [126509999114328] = SCRIPTS.NIGHTS99,

    -- Huss Valley
    [107535308163741] = SCRIPTS.HUSSVALLEY,
}

local function getScriptUrl()
    local gameId = game.GameId
    while gameId == 0 and game.PlaceId == 0 do
        task.wait()
        gameId = game.GameId
    end
    return byGameId[gameId] or byPlaceId[game.PlaceId]
end

-- Returns the payload source, or nil plus a message for the UI.
local function deliver(key)
    local url = getScriptUrl()
    if not url then
        return nil, ("Unsupported game. PlaceId=%s GameId=%s"):format(tostring(game.PlaceId), tostring(game.GameId))
    end

    status.Text = "Downloading script..."
    for attempt = 1, 3 do
        local source = fetch(url)
        if source then return source end
        task.wait(0.5)
    end

    return nil, "Could not download the script. Check your connection or executor."
end

-- [LOADER] The main thread waits for the key UI, then fetches and compiles the
--  payload. The payload itself runs in task.spawn so the Continue button and
--  the rest of the game thread are not blocked.
local function runLaunch()
    while true do
        while not launchRequest do
            task.wait(0.1)
        end

        local key = launchRequest
        launchRequest = nil

        status.Text = "Loading Synvextia..."
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Loading"

        local started = os.clock()
        local okCall, payload, err = pcall(deliver, key)
        if not okCall then
            payload, err = nil, tostring(payload)
        end

        if not payload then
            -- keep the UI alive so the key can be retried
            accepted = false
            status.Text = tostring(err or "Loader error")
            status.TextColor3 = COL_ERROR
            checkButton.Text = "Check Key"
            warn("[Synvextia] " .. tostring(err))
        else
            print(("[Synvextia] payload: %d bytes in %.1fs"):format(#payload, os.clock() - started))

            local chunk, compileErr = loadstring(payload)
            if not chunk then
                accepted = false
                status.Text = "Loader script failed to compile"
                status.TextColor3 = COL_ERROR
                checkButton.Text = "Check Key"
                warn("[Synvextia] compile error: " .. tostring(compileErr))
            else
                pcall(function() screenGui:Destroy() end)

                -- Let the pulse loop and any click/auto-login thread finish
                -- before spawning the payload thread.
                task.wait(0.3)

                task.spawn(function()
                    local okRun, runErr = pcall(chunk)
                    if okRun then
                        print(("[Synvextia] loader returned after %.1fs"):format(os.clock() - started))
                    else
                        warn(("[Synvextia] loader failed after %.1fs: %s"):format(os.clock() - started, tostring(runErr)))
                    end
                end)
                break
            end
        end
    end
end

local function checkKey(isAuto)
    if accepted then return end
    local key = normalizeKey(keyBox.Text)
    if key == "" then
        if not isAuto then
            status.Text = "Enter a key first"
            status.TextColor3 = COL_ERROR
        end
        return
    end
    -- [NOTE] Local key check.
    if VALID_KEYS[key] then
        accepted = true
        saveKey(key)
        status.Text = isAuto and "Saved key found! Logging in..." or "Key accepted!"
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Success"
        task.wait(0.6)
        launchRequest = key
    else
        status.Text = "Invalid key - join the server for one"
        status.TextColor3 = COL_ERROR
        if isAuto then
            clearSavedKey()
            keyBox.Text = ""
        end
    end
end

joinButton.MouseButton1Click:Connect(function()
    if busy then return end
    busy = true
    local copied = false
    local fns = {}
    if typeof(setclipboard) == "function" then table.insert(fns, setclipboard) end
    if typeof(writeclipboard) == "function" then table.insert(fns, writeclipboard) end
    table.insert(fns, function(t) return GuiService:SetClipboard(t) end)

    for _, fn in ipairs(fns) do
        local ok = pcall(fn, INVITE)
        if ok then copied = true break end
    end
    if not copied then
        keyBox.Text = INVITE
    end
    joinButton.Text = copied and "Copied! Paste in Discord" or "Invite in box - copy it"
    task.wait(1.8)
    joinButton.Text = "Copy Discord Invite"
    busy = false
end)

checkButton.MouseButton1Click:Connect(function() checkKey(false) end)
keyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then checkKey(false) end
end)

local lastAuto = 0
keyBox:GetPropertyChangedSignal("Text"):Connect(function()
    if accepted then return end
    local k = normalizeKey(keyBox.Text)
    if VALID_KEYS[k] and tick() - lastAuto > 1 then
        lastAuto = tick()
        checkKey(false)
    end
end)

task.spawn(function()
    local saved = loadSavedKey()
    if saved ~= "" then
        keyBox.Text = saved
        status.Text = "Saved key found! Logging in..."
        status.TextColor3 = COL_SUBTEXT
        task.wait(0.6)
        if not screenGui.Parent then return end
        checkKey(true)
    end
end)

task.spawn(function()
    while screenGui.Parent do
        local pulse = math.sin(tick() * 2) * 0.5 + 0.5
        joinGradient.Offset = Vector2.new(0, pulse * 0.6 - 0.3)
        RunService.RenderStepped:Wait()
    end
end)

-- The main thread waits for the key UI, then fetches and compiles the payload.
-- The payload runs in task.spawn so it does not block the UI or game thread.
runLaunch()



-- [HTTPGET #9]: https://raw.githubusercontent.com/SynvextiaHub/Loader/main/Syn
loadstring(game:HttpGet("https://raw.githubusercontent.com/SynvextiaHub/Loader./main/SYN"))()



-- [LOADSTRING #10] - Chunk: nil
loadstring(game:HttpGet("https://raw.githubusercontent.com/SynvextiaHub/Loader./main/SYN"))()



-- [HTTPGET #11]: https://raw.githubusercontent.com/SynvextiaHub/Loader./main/SYN
--[[
  Synvextia Key System -> per-game loader
  Key: syn2
  Preserves request-first fetch and task.spawn execution.
]]

print("[Synvextia] loader v2 (direct per-game URLs)")

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local GuiService = game:GetService("GuiService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local INVITE = "https://discord.gg/6YQagDhEqy"
local MESSAGE = "Join the server to get your key\nThere is no checkpoints"
local VALID_KEYS = {
    ["syn2"] = true,
}

local KEY_FILE = "synvextia_key.txt"

local function normalizeKey(s)
    return tostring(s or ""):gsub("%s+", "")
end

-- [NOTE] Some builds read getgenv().SCRIPT_KEY; set both names for compatibility.
local function saveKey(key)
    key = normalizeKey(key)
    if key == "" then return end
    pcall(function()
        if writefile then writefile(KEY_FILE, key) end
    end)
    pcall(function()
        getgenv().SCRIPT_KEY = key
        getgenv().SynvextiaKey = key
    end)
    pcall(function()
        _G.SCRIPT_KEY = key
        _G.SynvextiaKey = key
    end)
end

local function loadSavedKey()
    if typeof(isfile) == "function" and typeof(readfile) == "function" then
        local ok, is = pcall(function() return isfile(KEY_FILE) end)
        if ok and is then
            local ok2, contents = pcall(function() return readfile(KEY_FILE) end)
            if ok2 and contents then
                local k = normalizeKey(contents)
                if k ~= "" then return k end
            end
        end
    end
    if typeof(getgenv) == "function" then
        local ok, k = pcall(function() return getgenv().SCRIPT_KEY or getgenv().SynvextiaKey end)
        if ok and k and normalizeKey(k) ~= "" then return normalizeKey(k) end
    end
    if _G.SynvextiaKey and normalizeKey(_G.SynvextiaKey) ~= "" then
        return normalizeKey(_G.SynvextiaKey)
    end
    return ""
end

local function clearSavedKey()
    pcall(function()
        if typeof(delfile) == "function" and typeof(isfile) == "function" then
            if isfile(KEY_FILE) then delfile(KEY_FILE) end
        elseif writefile then
            writefile(KEY_FILE, "")
        end
    end)
    pcall(function() getgenv().SCRIPT_KEY = nil end)
    pcall(function() _G.SynvextiaKey = nil end)
end

local COL_BG_TOP = Color3.fromRGB(24, 25, 32)
local COL_BG_BOTTOM = Color3.fromRGB(12, 12, 17)
local COL_PANEL_TOP = Color3.fromRGB(48, 50, 58)
local COL_PANEL_BOTTOM = Color3.fromRGB(34, 36, 42)
local COL_ACCENT = Color3.fromRGB(88, 101, 242)
local COL_ACCENT_HOVER = Color3.fromRGB(108, 120, 255)
local COL_SUCCESS = Color3.fromRGB(35, 134, 78)
local COL_ERROR = Color3.fromRGB(178, 58, 72)
local COL_TEXT = Color3.fromRGB(245, 246, 250)
local COL_SUBTEXT = Color3.fromRGB(160, 165, 185)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "SynvextiaKeySystem"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 9999
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

local overlay = Instance.new("Frame")
overlay.Name = "Overlay"
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = COL_BG_BOTTOM
overlay.BackgroundTransparency = 1
overlay.BorderSizePixel = 0
overlay.ZIndex = 1
overlay.Parent = screenGui

local backdropGradient = Instance.new("UIGradient")
backdropGradient.Color = ColorSequence.new(COL_BG_TOP, COL_BG_BOTTOM)
backdropGradient.Rotation = 45
backdropGradient.Parent = overlay
TweenService:Create(overlay, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), { BackgroundTransparency = 0.25 }):Play()

local panel = Instance.new("Frame")
panel.Name = "Panel"
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Position = UDim2.fromScale(0.5, 0.5)
panel.Size = UDim2.new(0.9, 0, 0, 420)
panel.BackgroundColor3 = COL_PANEL_BOTTOM
panel.BorderSizePixel = 0
panel.ZIndex = 2
panel.Parent = overlay

local panelSize = Instance.new("UISizeConstraint")
panelSize.MaxSize = Vector2.new(660, 420)
panelSize.MinSize = Vector2.new(300, 420)
panelSize.Parent = panel

local panelGradient = Instance.new("UIGradient")
panelGradient.Color = ColorSequence.new(COL_PANEL_TOP, COL_PANEL_BOTTOM)
panelGradient.Rotation = 90
panelGradient.Parent = panel

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 18)
panelCorner.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Color = Color3.fromRGB(255, 255, 255)
panelStroke.Transparency = 0.85
panelStroke.Thickness = 1.5
panelStroke.Parent = panel

local accent = Instance.new("Frame")
accent.Name = "Accent"
accent.Size = UDim2.new(1, -80, 0, 6)
accent.Position = UDim2.new(0.5, 0, 0, 24)
accent.AnchorPoint = Vector2.new(0.5, 0)
accent.BackgroundColor3 = COL_ACCENT
accent.BorderSizePixel = 0
accent.ZIndex = 3
accent.Parent = panel
Instance.new("UICorner", accent).CornerRadius = UDim.new(1, 0)

local accentGradient = Instance.new("UIGradient")
accentGradient.Color = ColorSequence.new(Color3.fromRGB(120, 130, 255), COL_ACCENT)
accentGradient.Parent = accent

local wordmark = Instance.new("TextLabel")
wordmark.Name = "Wordmark"
wordmark.AnchorPoint = Vector2.new(0.5, 0)
wordmark.Position = UDim2.new(0.5, 0, 0, 44)
wordmark.Size = UDim2.new(1, -40, 0, 18)
wordmark.BackgroundTransparency = 1
wordmark.Text = "S Y N V E X T I A"
wordmark.TextColor3 = COL_ACCENT_HOVER
wordmark.TextSize = 14
wordmark.Font = Enum.Font.GothamBold
wordmark.TextTransparency = 0.25
wordmark.ZIndex = 3
wordmark.Parent = panel

local title = Instance.new("TextLabel")
title.Name = "Title"
title.AnchorPoint = Vector2.new(0.5, 0)
title.Position = UDim2.new(0.5, 0, 0, 70)
title.Size = UDim2.new(1, -50, 0, 40)
title.BackgroundTransparency = 1
title.Text = "Key System"
title.TextColor3 = COL_TEXT
title.TextSize = 30
title.Font = Enum.Font.GothamBold
title.ZIndex = 3
title.Parent = panel

local message = Instance.new("TextLabel")
message.Name = "Message"
message.AnchorPoint = Vector2.new(0.5, 0)
message.Position = UDim2.new(0.5, 0, 0, 108)
message.Size = UDim2.new(1, -50, 0, 52)
message.BackgroundTransparency = 1
message.Text = MESSAGE
message.TextColor3 = COL_SUBTEXT
message.TextWrapped = true
message.TextSize = 16
message.Font = Enum.Font.Gotham
message.TextXAlignment = Enum.TextXAlignment.Center
message.ZIndex = 3
message.Parent = panel

local joinButton = Instance.new("TextButton")
joinButton.Name = "JoinButton"
joinButton.AnchorPoint = Vector2.new(0.5, 0)
joinButton.Position = UDim2.new(0.5, 0, 0, 164)
joinButton.Size = UDim2.new(1, -100, 0, 50)
joinButton.BackgroundColor3 = COL_ACCENT
joinButton.BorderSizePixel = 0
joinButton.Text = "Copy Discord Invite"
joinButton.TextColor3 = Color3.new(1, 1, 1)
joinButton.TextSize = 22
joinButton.Font = Enum.Font.GothamBold
joinButton.AutoButtonColor = false
joinButton.ZIndex = 3
joinButton.Parent = panel
Instance.new("UICorner", joinButton).CornerRadius = UDim.new(0, 14)

local joinGradient = Instance.new("UIGradient")
joinGradient.Color = ColorSequence.new(COL_ACCENT_HOVER, COL_ACCENT)
joinGradient.Rotation = 90
joinGradient.Parent = joinButton

local joinScale = Instance.new("UIScale")
joinScale.Parent = joinButton
joinButton.MouseEnter:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
joinButton.MouseLeave:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local keyBox = Instance.new("TextBox")
keyBox.Name = "KeyBox"
keyBox.AnchorPoint = Vector2.new(0.5, 0)
keyBox.Position = UDim2.new(0.5, 0, 0, 236)
keyBox.Size = UDim2.new(1, -110, 0, 42)
keyBox.BackgroundColor3 = Color3.fromRGB(20, 21, 26)
keyBox.BackgroundTransparency = 0.25
keyBox.BorderSizePixel = 0
keyBox.ClearTextOnFocus = false
keyBox.Font = Enum.Font.Code
keyBox.PlaceholderText = "Paste your key here..."
keyBox.Text = ""
keyBox.TextColor3 = COL_TEXT
keyBox.PlaceholderColor3 = COL_SUBTEXT
keyBox.TextSize = 16
keyBox.TextXAlignment = Enum.TextXAlignment.Center
keyBox.ZIndex = 3
keyBox.Parent = panel
Instance.new("UICorner", keyBox).CornerRadius = UDim.new(0, 8)

local checkButton = Instance.new("TextButton")
checkButton.Name = "CheckButton"
checkButton.AnchorPoint = Vector2.new(0.5, 0)
checkButton.Position = UDim2.new(0.5, 0, 0, 296)
checkButton.Size = UDim2.new(1, -100, 0, 50)
checkButton.BackgroundColor3 = COL_SUCCESS
checkButton.BorderSizePixel = 0
checkButton.Text = "Check Key"
checkButton.TextColor3 = Color3.new(1, 1, 1)
checkButton.TextSize = 22
checkButton.Font = Enum.Font.GothamBold
checkButton.AutoButtonColor = false
checkButton.ZIndex = 3
checkButton.Parent = panel
Instance.new("UICorner", checkButton).CornerRadius = UDim.new(0, 14)

local checkScale = Instance.new("UIScale")
checkScale.Parent = checkButton
checkButton.MouseEnter:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
checkButton.MouseLeave:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local status = Instance.new("TextLabel")
status.Name = "Status"
status.AnchorPoint = Vector2.new(0.5, 0)
status.Position = UDim2.new(0.5, 0, 0, 360)
status.Size = UDim2.new(1, -40, 0, 20)
status.BackgroundTransparency = 1
status.Text = ""
status.TextColor3 = COL_SUBTEXT
status.TextSize = 14
status.Font = Enum.Font.Gotham
status.ZIndex = 3
status.Parent = panel

local busy = false
local accepted = false
local launchRequest = nil

-- [LOADER] Request-first fetch, then game:HttpGet fallback.
local function fetch(url)
    local req = (type(syn) == "table" and syn.request) or request or http_request
    if type(req) == "function" then
        local ok, res = pcall(req, { Url = url, Method = "GET" })
        if ok and type(res) == "table" and tonumber(res.StatusCode) == 200 and type(res.Body) == "string" and res.Body ~= "" then
            return res.Body
        end
    end

    local ok, source = pcall(game.HttpGet, game, url)
    if ok and type(source) == "string" and source ~= "" then
        return source
    end

    return nil
end

local SCRIPTS = {
    MM2        = "https://api.jnkie.com/api/v1/luascripts/public/f88bc27f071600baaa1afc246ffb6c53461c215a7db93c969959072152943cd5/download",
    DOORS      = "https://api.jnkie.com/api/v1/luascripts/public/7915991c0c868d1938aff55d370c8050e063cbcb8762a95fd405f21b8587ea2c/download",
    TIMEBOMB   = "https://api.jnkie.com/api/v1/luascripts/public/69a06a1de9966f3012fb2bd2cb8d5d2af674dc9125f4d0ba7b4fd323a8dce635/download",
    FORSAKEN   = "https://api.jnkie.com/api/v1/luascripts/public/7c4032d89f36d9fab5ac0076a4802086eebc9d17c223283ea042bc9753ebd2cc/download",
    DEADRAILS  = "https://api.jnkie.com/api/v1/luascripts/public/19ab1970bbdf3b967d63349f52d7967b0e7a39860a4e463f2f4771a165aa543e/download",
    VOLLEYBALL = "https://api.jnkie.com/api/v1/luascripts/public/41bf8158fc125b3d895f332771b5aeaed072c5b8ea16d8002d0878644fa3578f/download",
    NIGHTS99   = "https://api.jnkie.com/api/v1/luascripts/public/1238dbd70c6f460836b85fca2e3311debed55047f9e21b8207de07caf7867d0f/download",
    HUSSVALLEY = "https://api.jnkie.com/api/v1/luascripts/public/fafaa6d66f82d1f8448f07b70e342014c18adc491dda695c13c0547776342f7e/download",
}

local byGameId = {
    [6931042565] = SCRIPTS.VOLLEYBALL,
    [2440500124] = SCRIPTS.DOORS,
}

local byPlaceId = {
    -- Murder Mystery 2
    [142823291] = SCRIPTS.MM2,
    [335132309] = SCRIPTS.MM2,
    [636649648] = SCRIPTS.MM2,
    [80469437126309] = SCRIPTS.MM2,

    -- DOORS
    [6516141723] = SCRIPTS.DOORS,
    [6839171747] = SCRIPTS.DOORS,
    [10549820578] = SCRIPTS.DOORS,
    [12308344607] = SCRIPTS.DOORS,
    [87716067947993] = SCRIPTS.DOORS,
    [110258689672367] = SCRIPTS.DOORS,

    -- Timebomb Duels
    [11379739543] = SCRIPTS.TIMEBOMB,

    -- Forsaken
    [18687417158] = SCRIPTS.FORSAKEN,
    [83645629621104] = SCRIPTS.FORSAKEN,
    [86454545238517] = SCRIPTS.FORSAKEN,
    [94626476208514] = SCRIPTS.FORSAKEN,
    [106560117662077] = SCRIPTS.FORSAKEN,

    -- Dead Rails
    [70876832253163] = SCRIPTS.DEADRAILS,
    [74106709399219] = SCRIPTS.DEADRAILS,
    [96831577561553] = SCRIPTS.DEADRAILS,
    [110282088381749] = SCRIPTS.DEADRAILS,
    [111285651581407] = SCRIPTS.DEADRAILS,
    [116495829188952] = SCRIPTS.DEADRAILS,

    -- Volleyball Legends
    [73956553001240] = SCRIPTS.VOLLEYBALL,
    [74691681039273] = SCRIPTS.VOLLEYBALL,
    [85395484560711] = SCRIPTS.VOLLEYBALL,
    [86789627188240] = SCRIPTS.VOLLEYBALL,
    [96802054849934] = SCRIPTS.VOLLEYBALL,
    [102580589030177] = SCRIPTS.VOLLEYBALL,
    [103521881639626] = SCRIPTS.VOLLEYBALL,
    [109684591839194] = SCRIPTS.VOLLEYBALL,
    [117134837736236] = SCRIPTS.VOLLEYBALL,
    [134314141048307] = SCRIPTS.VOLLEYBALL,

    -- 99 Nights in the Forest
    [79546208627805] = SCRIPTS.NIGHTS99,
    [126509999114328] = SCRIPTS.NIGHTS99,

    -- Huss Valley
    [107535308163741] = SCRIPTS.HUSSVALLEY,
}

local function getScriptUrl()
    local gameId = game.GameId
    while gameId == 0 and game.PlaceId == 0 do
        task.wait()
        gameId = game.GameId
    end
    return byGameId[gameId] or byPlaceId[game.PlaceId]
end

-- Returns the payload source, or nil plus a message for the UI.
local function deliver(key)
    local url = getScriptUrl()
    if not url then
        return nil, ("Unsupported game. PlaceId=%s GameId=%s"):format(tostring(game.PlaceId), tostring(game.GameId))
    end

    status.Text = "Downloading script..."
    for attempt = 1, 3 do
        local source = fetch(url)
        if source then return source end
        task.wait(0.5)
    end

    return nil, "Could not download the script. Check your connection or executor."
end

-- [LOADER] The main thread waits for the key UI, then fetches and compiles the
--  payload. The payload itself runs in task.spawn so the Continue button and
--  the rest of the game thread are not blocked.
local function runLaunch()
    while true do
        while not launchRequest do
            task.wait(0.1)
        end

        local key = launchRequest
        launchRequest = nil

        status.Text = "Loading Synvextia..."
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Loading"

        local started = os.clock()
        local okCall, payload, err = pcall(deliver, key)
        if not okCall then
            payload, err = nil, tostring(payload)
        end

        if not payload then
            -- keep the UI alive so the key can be retried
            accepted = false
            status.Text = tostring(err or "Loader error")
            status.TextColor3 = COL_ERROR
            checkButton.Text = "Check Key"
            warn("[Synvextia] " .. tostring(err))
        else
            print(("[Synvextia] payload: %d bytes in %.1fs"):format(#payload, os.clock() - started))

            local chunk, compileErr = loadstring(payload)
            if not chunk then
                accepted = false
                status.Text = "Loader script failed to compile"
                status.TextColor3 = COL_ERROR
                checkButton.Text = "Check Key"
                warn("[Synvextia] compile error: " .. tostring(compileErr))
            else
                pcall(function() screenGui:Destroy() end)

                -- Let the pulse loop and any click/auto-login thread finish
                -- before spawning the payload thread.
                task.wait(0.3)

                task.spawn(function()
                    local okRun, runErr = pcall(chunk)
                    if okRun then
                        print(("[Synvextia] loader returned after %.1fs"):format(os.clock() - started))
                    else
                        warn(("[Synvextia] loader failed after %.1fs: %s"):format(os.clock() - started, tostring(runErr)))
                    end
                end)
                break
            end
        end
    end
end

local function checkKey(isAuto)
    if accepted then return end
    local key = normalizeKey(keyBox.Text)
    if key == "" then
        if not isAuto then
            status.Text = "Enter a key first"
            status.TextColor3 = COL_ERROR
        end
        return
    end
    -- [NOTE] Local key check.
    if VALID_KEYS[key] then
        accepted = true
        saveKey(key)
        status.Text = isAuto and "Saved key found! Logging in..." or "Key accepted!"
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Success"
        task.wait(0.6)
        launchRequest = key
    else
        status.Text = "Invalid key - join the server for one"
        status.TextColor3 = COL_ERROR
        if isAuto then
            clearSavedKey()
            keyBox.Text = ""
        end
    end
end

joinButton.MouseButton1Click:Connect(function()
    if busy then return end
    busy = true
    local copied = false
    local fns = {}
    if typeof(setclipboard) == "function" then table.insert(fns, setclipboard) end
    if typeof(writeclipboard) == "function" then table.insert(fns, writeclipboard) end
    table.insert(fns, function(t) return GuiService:SetClipboard(t) end)

    for _, fn in ipairs(fns) do
        local ok = pcall(fn, INVITE)
        if ok then copied = true break end
    end
    if not copied then
        keyBox.Text = INVITE
    end
    joinButton.Text = copied and "Copied! Paste in Discord" or "Invite in box - copy it"
    task.wait(1.8)
    joinButton.Text = "Copy Discord Invite"
    busy = false
end)

checkButton.MouseButton1Click:Connect(function() checkKey(false) end)
keyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then checkKey(false) end
end)

local lastAuto = 0
keyBox:GetPropertyChangedSignal("Text"):Connect(function()
    if accepted then return end
    local k = normalizeKey(keyBox.Text)
    if VALID_KEYS[k] and tick() - lastAuto > 1 then
        lastAuto = tick()
        checkKey(false)
    end
end)

task.spawn(function()
    local saved = loadSavedKey()
    if saved ~= "" then
        keyBox.Text = saved
        status.Text = "Saved key found! Logging in..."
        status.TextColor3 = COL_SUBTEXT
        task.wait(0.6)
        if not screenGui.Parent then return end
        checkKey(true)
    end
end)

task.spawn(function()
    while screenGui.Parent do
        local pulse = math.sin(tick() * 2) * 0.5 + 0.5
        joinGradient.Offset = Vector2.new(0, pulse * 0.6 - 0.3)
        RunService.RenderStepped:Wait()
    end
end)

-- The main thread waits for the key UI, then fetches and compiles the payload.
-- The payload runs in task.spawn so it does not block the UI or game thread.
runLaunch()



-- [LOADSTRING #12] - Chunk: nil
--[[
  Synvextia Key System -> per-game loader
  Key: syn2
  Preserves request-first fetch and task.spawn execution.
]]

print("[Synvextia] loader v2 (direct per-game URLs)")

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local GuiService = game:GetService("GuiService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local INVITE = "https://discord.gg/6YQagDhEqy"
local MESSAGE = "Join the server to get your key\nThere is no checkpoints"
local VALID_KEYS = {
    ["syn2"] = true,
}

local KEY_FILE = "synvextia_key.txt"

local function normalizeKey(s)
    return tostring(s or ""):gsub("%s+", "")
end

-- [NOTE] Some builds read getgenv().SCRIPT_KEY; set both names for compatibility.
local function saveKey(key)
    key = normalizeKey(key)
    if key == "" then return end
    pcall(function()
        if writefile then writefile(KEY_FILE, key) end
    end)
    pcall(function()
        getgenv().SCRIPT_KEY = key
        getgenv().SynvextiaKey = key
    end)
    pcall(function()
        _G.SCRIPT_KEY = key
        _G.SynvextiaKey = key
    end)
end

local function loadSavedKey()
    if typeof(isfile) == "function" and typeof(readfile) == "function" then
        local ok, is = pcall(function() return isfile(KEY_FILE) end)
        if ok and is then
            local ok2, contents = pcall(function() return readfile(KEY_FILE) end)
            if ok2 and contents then
                local k = normalizeKey(contents)
                if k ~= "" then return k end
            end
        end
    end
    if typeof(getgenv) == "function" then
        local ok, k = pcall(function() return getgenv().SCRIPT_KEY or getgenv().SynvextiaKey end)
        if ok and k and normalizeKey(k) ~= "" then return normalizeKey(k) end
    end
    if _G.SynvextiaKey and normalizeKey(_G.SynvextiaKey) ~= "" then
        return normalizeKey(_G.SynvextiaKey)
    end
    return ""
end

local function clearSavedKey()
    pcall(function()
        if typeof(delfile) == "function" and typeof(isfile) == "function" then
            if isfile(KEY_FILE) then delfile(KEY_FILE) end
        elseif writefile then
            writefile(KEY_FILE, "")
        end
    end)
    pcall(function() getgenv().SCRIPT_KEY = nil end)
    pcall(function() _G.SynvextiaKey = nil end)
end

local COL_BG_TOP = Color3.fromRGB(24, 25, 32)
local COL_BG_BOTTOM = Color3.fromRGB(12, 12, 17)
local COL_PANEL_TOP = Color3.fromRGB(48, 50, 58)
local COL_PANEL_BOTTOM = Color3.fromRGB(34, 36, 42)
local COL_ACCENT = Color3.fromRGB(88, 101, 242)
local COL_ACCENT_HOVER = Color3.fromRGB(108, 120, 255)
local COL_SUCCESS = Color3.fromRGB(35, 134, 78)
local COL_ERROR = Color3.fromRGB(178, 58, 72)
local COL_TEXT = Color3.fromRGB(245, 246, 250)
local COL_SUBTEXT = Color3.fromRGB(160, 165, 185)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "SynvextiaKeySystem"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 9999
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

local overlay = Instance.new("Frame")
overlay.Name = "Overlay"
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = COL_BG_BOTTOM
overlay.BackgroundTransparency = 1
overlay.BorderSizePixel = 0
overlay.ZIndex = 1
overlay.Parent = screenGui

local backdropGradient = Instance.new("UIGradient")
backdropGradient.Color = ColorSequence.new(COL_BG_TOP, COL_BG_BOTTOM)
backdropGradient.Rotation = 45
backdropGradient.Parent = overlay
TweenService:Create(overlay, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), { BackgroundTransparency = 0.25 }):Play()

local panel = Instance.new("Frame")
panel.Name = "Panel"
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Position = UDim2.fromScale(0.5, 0.5)
panel.Size = UDim2.new(0.9, 0, 0, 420)
panel.BackgroundColor3 = COL_PANEL_BOTTOM
panel.BorderSizePixel = 0
panel.ZIndex = 2
panel.Parent = overlay

local panelSize = Instance.new("UISizeConstraint")
panelSize.MaxSize = Vector2.new(660, 420)
panelSize.MinSize = Vector2.new(300, 420)
panelSize.Parent = panel

local panelGradient = Instance.new("UIGradient")
panelGradient.Color = ColorSequence.new(COL_PANEL_TOP, COL_PANEL_BOTTOM)
panelGradient.Rotation = 90
panelGradient.Parent = panel

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 18)
panelCorner.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Color = Color3.fromRGB(255, 255, 255)
panelStroke.Transparency = 0.85
panelStroke.Thickness = 1.5
panelStroke.Parent = panel

local accent = Instance.new("Frame")
accent.Name = "Accent"
accent.Size = UDim2.new(1, -80, 0, 6)
accent.Position = UDim2.new(0.5, 0, 0, 24)
accent.AnchorPoint = Vector2.new(0.5, 0)
accent.BackgroundColor3 = COL_ACCENT
accent.BorderSizePixel = 0
accent.ZIndex = 3
accent.Parent = panel
Instance.new("UICorner", accent).CornerRadius = UDim.new(1, 0)

local accentGradient = Instance.new("UIGradient")
accentGradient.Color = ColorSequence.new(Color3.fromRGB(120, 130, 255), COL_ACCENT)
accentGradient.Parent = accent

local wordmark = Instance.new("TextLabel")
wordmark.Name = "Wordmark"
wordmark.AnchorPoint = Vector2.new(0.5, 0)
wordmark.Position = UDim2.new(0.5, 0, 0, 44)
wordmark.Size = UDim2.new(1, -40, 0, 18)
wordmark.BackgroundTransparency = 1
wordmark.Text = "S Y N V E X T I A"
wordmark.TextColor3 = COL_ACCENT_HOVER
wordmark.TextSize = 14
wordmark.Font = Enum.Font.GothamBold
wordmark.TextTransparency = 0.25
wordmark.ZIndex = 3
wordmark.Parent = panel

local title = Instance.new("TextLabel")
title.Name = "Title"
title.AnchorPoint = Vector2.new(0.5, 0)
title.Position = UDim2.new(0.5, 0, 0, 70)
title.Size = UDim2.new(1, -50, 0, 40)
title.BackgroundTransparency = 1
title.Text = "Key System"
title.TextColor3 = COL_TEXT
title.TextSize = 30
title.Font = Enum.Font.GothamBold
title.ZIndex = 3
title.Parent = panel

local message = Instance.new("TextLabel")
message.Name = "Message"
message.AnchorPoint = Vector2.new(0.5, 0)
message.Position = UDim2.new(0.5, 0, 0, 108)
message.Size = UDim2.new(1, -50, 0, 52)
message.BackgroundTransparency = 1
message.Text = MESSAGE
message.TextColor3 = COL_SUBTEXT
message.TextWrapped = true
message.TextSize = 16
message.Font = Enum.Font.Gotham
message.TextXAlignment = Enum.TextXAlignment.Center
message.ZIndex = 3
message.Parent = panel

local joinButton = Instance.new("TextButton")
joinButton.Name = "JoinButton"
joinButton.AnchorPoint = Vector2.new(0.5, 0)
joinButton.Position = UDim2.new(0.5, 0, 0, 164)
joinButton.Size = UDim2.new(1, -100, 0, 50)
joinButton.BackgroundColor3 = COL_ACCENT
joinButton.BorderSizePixel = 0
joinButton.Text = "Copy Discord Invite"
joinButton.TextColor3 = Color3.new(1, 1, 1)
joinButton.TextSize = 22
joinButton.Font = Enum.Font.GothamBold
joinButton.AutoButtonColor = false
joinButton.ZIndex = 3
joinButton.Parent = panel
Instance.new("UICorner", joinButton).CornerRadius = UDim.new(0, 14)

local joinGradient = Instance.new("UIGradient")
joinGradient.Color = ColorSequence.new(COL_ACCENT_HOVER, COL_ACCENT)
joinGradient.Rotation = 90
joinGradient.Parent = joinButton

local joinScale = Instance.new("UIScale")
joinScale.Parent = joinButton
joinButton.MouseEnter:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
joinButton.MouseLeave:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local keyBox = Instance.new("TextBox")
keyBox.Name = "KeyBox"
keyBox.AnchorPoint = Vector2.new(0.5, 0)
keyBox.Position = UDim2.new(0.5, 0, 0, 236)
keyBox.Size = UDim2.new(1, -110, 0, 42)
keyBox.BackgroundColor3 = Color3.fromRGB(20, 21, 26)
keyBox.BackgroundTransparency = 0.25
keyBox.BorderSizePixel = 0
keyBox.ClearTextOnFocus = false
keyBox.Font = Enum.Font.Code
keyBox.PlaceholderText = "Paste your key here..."
keyBox.Text = ""
keyBox.TextColor3 = COL_TEXT
keyBox.PlaceholderColor3 = COL_SUBTEXT
keyBox.TextSize = 16
keyBox.TextXAlignment = Enum.TextXAlignment.Center
keyBox.ZIndex = 3
keyBox.Parent = panel
Instance.new("UICorner", keyBox).CornerRadius = UDim.new(0, 8)

local checkButton = Instance.new("TextButton")
checkButton.Name = "CheckButton"
checkButton.AnchorPoint = Vector2.new(0.5, 0)
checkButton.Position = UDim2.new(0.5, 0, 0, 296)
checkButton.Size = UDim2.new(1, -100, 0, 50)
checkButton.BackgroundColor3 = COL_SUCCESS
checkButton.BorderSizePixel = 0
checkButton.Text = "Check Key"
checkButton.TextColor3 = Color3.new(1, 1, 1)
checkButton.TextSize = 22
checkButton.Font = Enum.Font.GothamBold
checkButton.AutoButtonColor = false
checkButton.ZIndex = 3
checkButton.Parent = panel
Instance.new("UICorner", checkButton).CornerRadius = UDim.new(0, 14)

local checkScale = Instance.new("UIScale")
checkScale.Parent = checkButton
checkButton.MouseEnter:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
checkButton.MouseLeave:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local status = Instance.new("TextLabel")
status.Name = "Status"
status.AnchorPoint = Vector2.new(0.5, 0)
status.Position = UDim2.new(0.5, 0, 0, 360)
status.Size = UDim2.new(1, -40, 0, 20)
status.BackgroundTransparency = 1
status.Text = ""
status.TextColor3 = COL_SUBTEXT
status.TextSize = 14
status.Font = Enum.Font.Gotham
status.ZIndex = 3
status.Parent = panel

local busy = false
local accepted = false
local launchRequest = nil

-- [LOADER] Request-first fetch, then game:HttpGet fallback.
local function fetch(url)
    local req = (type(syn) == "table" and syn.request) or request or http_request
    if type(req) == "function" then
        local ok, res = pcall(req, { Url = url, Method = "GET" })
        if ok and type(res) == "table" and tonumber(res.StatusCode) == 200 and type(res.Body) == "string" and res.Body ~= "" then
            return res.Body
        end
    end

    local ok, source = pcall(game.HttpGet, game, url)
    if ok and type(source) == "string" and source ~= "" then
        return source
    end

    return nil
end

local SCRIPTS = {
    MM2        = "https://api.jnkie.com/api/v1/luascripts/public/f88bc27f071600baaa1afc246ffb6c53461c215a7db93c969959072152943cd5/download",
    DOORS      = "https://api.jnkie.com/api/v1/luascripts/public/7915991c0c868d1938aff55d370c8050e063cbcb8762a95fd405f21b8587ea2c/download",
    TIMEBOMB   = "https://api.jnkie.com/api/v1/luascripts/public/69a06a1de9966f3012fb2bd2cb8d5d2af674dc9125f4d0ba7b4fd323a8dce635/download",
    FORSAKEN   = "https://api.jnkie.com/api/v1/luascripts/public/7c4032d89f36d9fab5ac0076a4802086eebc9d17c223283ea042bc9753ebd2cc/download",
    DEADRAILS  = "https://api.jnkie.com/api/v1/luascripts/public/19ab1970bbdf3b967d63349f52d7967b0e7a39860a4e463f2f4771a165aa543e/download",
    VOLLEYBALL = "https://api.jnkie.com/api/v1/luascripts/public/41bf8158fc125b3d895f332771b5aeaed072c5b8ea16d8002d0878644fa3578f/download",
    NIGHTS99   = "https://api.jnkie.com/api/v1/luascripts/public/1238dbd70c6f460836b85fca2e3311debed55047f9e21b8207de07caf7867d0f/download",
    HUSSVALLEY = "https://api.jnkie.com/api/v1/luascripts/public/fafaa6d66f82d1f8448f07b70e342014c18adc491dda695c13c0547776342f7e/download",
}

local byGameId = {
    [6931042565] = SCRIPTS.VOLLEYBALL,
    [2440500124] = SCRIPTS.DOORS,
}

local byPlaceId = {
    -- Murder Mystery 2
    [142823291] = SCRIPTS.MM2,
    [335132309] = SCRIPTS.MM2,
    [636649648] = SCRIPTS.MM2,
    [80469437126309] = SCRIPTS.MM2,

    -- DOORS
    [6516141723] = SCRIPTS.DOORS,
    [6839171747] = SCRIPTS.DOORS,
    [10549820578] = SCRIPTS.DOORS,
    [12308344607] = SCRIPTS.DOORS,
    [87716067947993] = SCRIPTS.DOORS,
    [110258689672367] = SCRIPTS.DOORS,

    -- Timebomb Duels
    [11379739543] = SCRIPTS.TIMEBOMB,

    -- Forsaken
    [18687417158] = SCRIPTS.FORSAKEN,
    [83645629621104] = SCRIPTS.FORSAKEN,
    [86454545238517] = SCRIPTS.FORSAKEN,
    [94626476208514] = SCRIPTS.FORSAKEN,
    [106560117662077] = SCRIPTS.FORSAKEN,

    -- Dead Rails
    [70876832253163] = SCRIPTS.DEADRAILS,
    [74106709399219] = SCRIPTS.DEADRAILS,
    [96831577561553] = SCRIPTS.DEADRAILS,
    [110282088381749] = SCRIPTS.DEADRAILS,
    [111285651581407] = SCRIPTS.DEADRAILS,
    [116495829188952] = SCRIPTS.DEADRAILS,

    -- Volleyball Legends
    [73956553001240] = SCRIPTS.VOLLEYBALL,
    [74691681039273] = SCRIPTS.VOLLEYBALL,
    [85395484560711] = SCRIPTS.VOLLEYBALL,
    [86789627188240] = SCRIPTS.VOLLEYBALL,
    [96802054849934] = SCRIPTS.VOLLEYBALL,
    [102580589030177] = SCRIPTS.VOLLEYBALL,
    [103521881639626] = SCRIPTS.VOLLEYBALL,
    [109684591839194] = SCRIPTS.VOLLEYBALL,
    [117134837736236] = SCRIPTS.VOLLEYBALL,
    [134314141048307] = SCRIPTS.VOLLEYBALL,

    -- 99 Nights in the Forest
    [79546208627805] = SCRIPTS.NIGHTS99,
    [126509999114328] = SCRIPTS.NIGHTS99,

    -- Huss Valley
    [107535308163741] = SCRIPTS.HUSSVALLEY,
}

local function getScriptUrl()
    local gameId = game.GameId
    while gameId == 0 and game.PlaceId == 0 do
        task.wait()
        gameId = game.GameId
    end
    return byGameId[gameId] or byPlaceId[game.PlaceId]
end

-- Returns the payload source, or nil plus a message for the UI.
local function deliver(key)
    local url = getScriptUrl()
    if not url then
        return nil, ("Unsupported game. PlaceId=%s GameId=%s"):format(tostring(game.PlaceId), tostring(game.GameId))
    end

    status.Text = "Downloading script..."
    for attempt = 1, 3 do
        local source = fetch(url)
        if source then return source end
        task.wait(0.5)
    end

    return nil, "Could not download the script. Check your connection or executor."
end

-- [LOADER] The main thread waits for the key UI, then fetches and compiles the
--  payload. The payload itself runs in task.spawn so the Continue button and
--  the rest of the game thread are not blocked.
local function runLaunch()
    while true do
        while not launchRequest do
            task.wait(0.1)
        end

        local key = launchRequest
        launchRequest = nil

        status.Text = "Loading Synvextia..."
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Loading"

        local started = os.clock()
        local okCall, payload, err = pcall(deliver, key)
        if not okCall then
            payload, err = nil, tostring(payload)
        end

        if not payload then
            -- keep the UI alive so the key can be retried
            accepted = false
            status.Text = tostring(err or "Loader error")
            status.TextColor3 = COL_ERROR
            checkButton.Text = "Check Key"
            warn("[Synvextia] " .. tostring(err))
        else
            print(("[Synvextia] payload: %d bytes in %.1fs"):format(#payload, os.clock() - started))

            local chunk, compileErr = loadstring(payload)
            if not chunk then
                accepted = false
                status.Text = "Loader script failed to compile"
                status.TextColor3 = COL_ERROR
                checkButton.Text = "Check Key"
                warn("[Synvextia] compile error: " .. tostring(compileErr))
            else
                pcall(function() screenGui:Destroy() end)

                -- Let the pulse loop and any click/auto-login thread finish
                -- before spawning the payload thread.
                task.wait(0.3)

                task.spawn(function()
                    local okRun, runErr = pcall(chunk)
                    if okRun then
                        print(("[Synvextia] loader returned after %.1fs"):format(os.clock() - started))
                    else
                        warn(("[Synvextia] loader failed after %.1fs: %s"):format(os.clock() - started, tostring(runErr)))
                    end
                end)
                break
            end
        end
    end
end

local function checkKey(isAuto)
    if accepted then return end
    local key = normalizeKey(keyBox.Text)
    if key == "" then
        if not isAuto then
            status.Text = "Enter a key first"
            status.TextColor3 = COL_ERROR
        end
        return
    end
    -- [NOTE] Local key check.
    if VALID_KEYS[key] then
        accepted = true
        saveKey(key)
        status.Text = isAuto and "Saved key found! Logging in..." or "Key accepted!"
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Success"
        task.wait(0.6)
        launchRequest = key
    else
        status.Text = "Invalid key - join the server for one"
        status.TextColor3 = COL_ERROR
        if isAuto then
            clearSavedKey()
            keyBox.Text = ""
        end
    end
end

joinButton.MouseButton1Click:Connect(function()
    if busy then return end
    busy = true
    local copied = false
    local fns = {}
    if typeof(setclipboard) == "function" then table.insert(fns, setclipboard) end
    if typeof(writeclipboard) == "function" then table.insert(fns, writeclipboard) end
    table.insert(fns, function(t) return GuiService:SetClipboard(t) end)

    for _, fn in ipairs(fns) do
        local ok = pcall(fn, INVITE)
        if ok then copied = true break end
    end
    if not copied then
        keyBox.Text = INVITE
    end
    joinButton.Text = copied and "Copied! Paste in Discord" or "Invite in box - copy it"
    task.wait(1.8)
    joinButton.Text = "Copy Discord Invite"
    busy = false
end)

checkButton.MouseButton1Click:Connect(function() checkKey(false) end)
keyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then checkKey(false) end
end)

local lastAuto = 0
keyBox:GetPropertyChangedSignal("Text"):Connect(function()
    if accepted then return end
    local k = normalizeKey(keyBox.Text)
    if VALID_KEYS[k] and tick() - lastAuto > 1 then
        lastAuto = tick()
        checkKey(false)
    end
end)

task.spawn(function()
    local saved = loadSavedKey()
    if saved ~= "" then
        keyBox.Text = saved
        status.Text = "Saved key found! Logging in..."
        status.TextColor3 = COL_SUBTEXT
        task.wait(0.6)
        if not screenGui.Parent then return end
        checkKey(true)
    end
end)

task.spawn(function()
    while screenGui.Parent do
        local pulse = math.sin(tick() * 2) * 0.5 + 0.5
        joinGradient.Offset = Vector2.new(0, pulse * 0.6 - 0.3)
        RunService.RenderStepped:Wait()
    end
end)

-- The main thread waits for the key UI, then fetches and compiles the payload.
-- The payload runs in task.spawn so it does not block the UI or game thread.
runLaunch()



-- [HTTPGET #13]: https://raw.githubusercontent.com/SynvextiaHub/Loader./main/SYN
--[[
  Synvextia Key System -> per-game loader
  Key: syn2
  Preserves request-first fetch and task.spawn execution.
]]

print("[Synvextia] loader v2 (direct per-game URLs)")

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local GuiService = game:GetService("GuiService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local INVITE = "https://discord.gg/6YQagDhEqy"
local MESSAGE = "Join the server to get your key\nThere is no checkpoints"
local VALID_KEYS = {
    ["syn2"] = true,
}

local KEY_FILE = "synvextia_key.txt"

local function normalizeKey(s)
    return tostring(s or ""):gsub("%s+", "")
end

-- [NOTE] Some builds read getgenv().SCRIPT_KEY; set both names for compatibility.
local function saveKey(key)
    key = normalizeKey(key)
    if key == "" then return end
    pcall(function()
        if writefile then writefile(KEY_FILE, key) end
    end)
    pcall(function()
        getgenv().SCRIPT_KEY = key
        getgenv().SynvextiaKey = key
    end)
    pcall(function()
        _G.SCRIPT_KEY = key
        _G.SynvextiaKey = key
    end)
end

local function loadSavedKey()
    if typeof(isfile) == "function" and typeof(readfile) == "function" then
        local ok, is = pcall(function() return isfile(KEY_FILE) end)
        if ok and is then
            local ok2, contents = pcall(function() return readfile(KEY_FILE) end)
            if ok2 and contents then
                local k = normalizeKey(contents)
                if k ~= "" then return k end
            end
        end
    end
    if typeof(getgenv) == "function" then
        local ok, k = pcall(function() return getgenv().SCRIPT_KEY or getgenv().SynvextiaKey end)
        if ok and k and normalizeKey(k) ~= "" then return normalizeKey(k) end
    end
    if _G.SynvextiaKey and normalizeKey(_G.SynvextiaKey) ~= "" then
        return normalizeKey(_G.SynvextiaKey)
    end
    return ""
end

local function clearSavedKey()
    pcall(function()
        if typeof(delfile) == "function" and typeof(isfile) == "function" then
            if isfile(KEY_FILE) then delfile(KEY_FILE) end
        elseif writefile then
            writefile(KEY_FILE, "")
        end
    end)
    pcall(function() getgenv().SCRIPT_KEY = nil end)
    pcall(function() _G.SynvextiaKey = nil end)
end

local COL_BG_TOP = Color3.fromRGB(24, 25, 32)
local COL_BG_BOTTOM = Color3.fromRGB(12, 12, 17)
local COL_PANEL_TOP = Color3.fromRGB(48, 50, 58)
local COL_PANEL_BOTTOM = Color3.fromRGB(34, 36, 42)
local COL_ACCENT = Color3.fromRGB(88, 101, 242)
local COL_ACCENT_HOVER = Color3.fromRGB(108, 120, 255)
local COL_SUCCESS = Color3.fromRGB(35, 134, 78)
local COL_ERROR = Color3.fromRGB(178, 58, 72)
local COL_TEXT = Color3.fromRGB(245, 246, 250)
local COL_SUBTEXT = Color3.fromRGB(160, 165, 185)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "SynvextiaKeySystem"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 9999
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

local overlay = Instance.new("Frame")
overlay.Name = "Overlay"
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = COL_BG_BOTTOM
overlay.BackgroundTransparency = 1
overlay.BorderSizePixel = 0
overlay.ZIndex = 1
overlay.Parent = screenGui

local backdropGradient = Instance.new("UIGradient")
backdropGradient.Color = ColorSequence.new(COL_BG_TOP, COL_BG_BOTTOM)
backdropGradient.Rotation = 45
backdropGradient.Parent = overlay
TweenService:Create(overlay, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), { BackgroundTransparency = 0.25 }):Play()

local panel = Instance.new("Frame")
panel.Name = "Panel"
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Position = UDim2.fromScale(0.5, 0.5)
panel.Size = UDim2.new(0.9, 0, 0, 420)
panel.BackgroundColor3 = COL_PANEL_BOTTOM
panel.BorderSizePixel = 0
panel.ZIndex = 2
panel.Parent = overlay

local panelSize = Instance.new("UISizeConstraint")
panelSize.MaxSize = Vector2.new(660, 420)
panelSize.MinSize = Vector2.new(300, 420)
panelSize.Parent = panel

local panelGradient = Instance.new("UIGradient")
panelGradient.Color = ColorSequence.new(COL_PANEL_TOP, COL_PANEL_BOTTOM)
panelGradient.Rotation = 90
panelGradient.Parent = panel

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 18)
panelCorner.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Color = Color3.fromRGB(255, 255, 255)
panelStroke.Transparency = 0.85
panelStroke.Thickness = 1.5
panelStroke.Parent = panel

local accent = Instance.new("Frame")
accent.Name = "Accent"
accent.Size = UDim2.new(1, -80, 0, 6)
accent.Position = UDim2.new(0.5, 0, 0, 24)
accent.AnchorPoint = Vector2.new(0.5, 0)
accent.BackgroundColor3 = COL_ACCENT
accent.BorderSizePixel = 0
accent.ZIndex = 3
accent.Parent = panel
Instance.new("UICorner", accent).CornerRadius = UDim.new(1, 0)

local accentGradient = Instance.new("UIGradient")
accentGradient.Color = ColorSequence.new(Color3.fromRGB(120, 130, 255), COL_ACCENT)
accentGradient.Parent = accent

local wordmark = Instance.new("TextLabel")
wordmark.Name = "Wordmark"
wordmark.AnchorPoint = Vector2.new(0.5, 0)
wordmark.Position = UDim2.new(0.5, 0, 0, 44)
wordmark.Size = UDim2.new(1, -40, 0, 18)
wordmark.BackgroundTransparency = 1
wordmark.Text = "S Y N V E X T I A"
wordmark.TextColor3 = COL_ACCENT_HOVER
wordmark.TextSize = 14
wordmark.Font = Enum.Font.GothamBold
wordmark.TextTransparency = 0.25
wordmark.ZIndex = 3
wordmark.Parent = panel

local title = Instance.new("TextLabel")
title.Name = "Title"
title.AnchorPoint = Vector2.new(0.5, 0)
title.Position = UDim2.new(0.5, 0, 0, 70)
title.Size = UDim2.new(1, -50, 0, 40)
title.BackgroundTransparency = 1
title.Text = "Key System"
title.TextColor3 = COL_TEXT
title.TextSize = 30
title.Font = Enum.Font.GothamBold
title.ZIndex = 3
title.Parent = panel

local message = Instance.new("TextLabel")
message.Name = "Message"
message.AnchorPoint = Vector2.new(0.5, 0)
message.Position = UDim2.new(0.5, 0, 0, 108)
message.Size = UDim2.new(1, -50, 0, 52)
message.BackgroundTransparency = 1
message.Text = MESSAGE
message.TextColor3 = COL_SUBTEXT
message.TextWrapped = true
message.TextSize = 16
message.Font = Enum.Font.Gotham
message.TextXAlignment = Enum.TextXAlignment.Center
message.ZIndex = 3
message.Parent = panel

local joinButton = Instance.new("TextButton")
joinButton.Name = "JoinButton"
joinButton.AnchorPoint = Vector2.new(0.5, 0)
joinButton.Position = UDim2.new(0.5, 0, 0, 164)
joinButton.Size = UDim2.new(1, -100, 0, 50)
joinButton.BackgroundColor3 = COL_ACCENT
joinButton.BorderSizePixel = 0
joinButton.Text = "Copy Discord Invite"
joinButton.TextColor3 = Color3.new(1, 1, 1)
joinButton.TextSize = 22
joinButton.Font = Enum.Font.GothamBold
joinButton.AutoButtonColor = false
joinButton.ZIndex = 3
joinButton.Parent = panel
Instance.new("UICorner", joinButton).CornerRadius = UDim.new(0, 14)

local joinGradient = Instance.new("UIGradient")
joinGradient.Color = ColorSequence.new(COL_ACCENT_HOVER, COL_ACCENT)
joinGradient.Rotation = 90
joinGradient.Parent = joinButton

local joinScale = Instance.new("UIScale")
joinScale.Parent = joinButton
joinButton.MouseEnter:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
joinButton.MouseLeave:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local keyBox = Instance.new("TextBox")
keyBox.Name = "KeyBox"
keyBox.AnchorPoint = Vector2.new(0.5, 0)
keyBox.Position = UDim2.new(0.5, 0, 0, 236)
keyBox.Size = UDim2.new(1, -110, 0, 42)
keyBox.BackgroundColor3 = Color3.fromRGB(20, 21, 26)
keyBox.BackgroundTransparency = 0.25
keyBox.BorderSizePixel = 0
keyBox.ClearTextOnFocus = false
keyBox.Font = Enum.Font.Code
keyBox.PlaceholderText = "Paste your key here..."
keyBox.Text = ""
keyBox.TextColor3 = COL_TEXT
keyBox.PlaceholderColor3 = COL_SUBTEXT
keyBox.TextSize = 16
keyBox.TextXAlignment = Enum.TextXAlignment.Center
keyBox.ZIndex = 3
keyBox.Parent = panel
Instance.new("UICorner", keyBox).CornerRadius = UDim.new(0, 8)

local checkButton = Instance.new("TextButton")
checkButton.Name = "CheckButton"
checkButton.AnchorPoint = Vector2.new(0.5, 0)
checkButton.Position = UDim2.new(0.5, 0, 0, 296)
checkButton.Size = UDim2.new(1, -100, 0, 50)
checkButton.BackgroundColor3 = COL_SUCCESS
checkButton.BorderSizePixel = 0
checkButton.Text = "Check Key"
checkButton.TextColor3 = Color3.new(1, 1, 1)
checkButton.TextSize = 22
checkButton.Font = Enum.Font.GothamBold
checkButton.AutoButtonColor = false
checkButton.ZIndex = 3
checkButton.Parent = panel
Instance.new("UICorner", checkButton).CornerRadius = UDim.new(0, 14)

local checkScale = Instance.new("UIScale")
checkScale.Parent = checkButton
checkButton.MouseEnter:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
checkButton.MouseLeave:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local status = Instance.new("TextLabel")
status.Name = "Status"
status.AnchorPoint = Vector2.new(0.5, 0)
status.Position = UDim2.new(0.5, 0, 0, 360)
status.Size = UDim2.new(1, -40, 0, 20)
status.BackgroundTransparency = 1
status.Text = ""
status.TextColor3 = COL_SUBTEXT
status.TextSize = 14
status.Font = Enum.Font.Gotham
status.ZIndex = 3
status.Parent = panel

local busy = false
local accepted = false
local launchRequest = nil

-- [LOADER] Request-first fetch, then game:HttpGet fallback.
local function fetch(url)
    local req = (type(syn) == "table" and syn.request) or request or http_request
    if type(req) == "function" then
        local ok, res = pcall(req, { Url = url, Method = "GET" })
        if ok and type(res) == "table" and tonumber(res.StatusCode) == 200 and type(res.Body) == "string" and res.Body ~= "" then
            return res.Body
        end
    end

    local ok, source = pcall(game.HttpGet, game, url)
    if ok and type(source) == "string" and source ~= "" then
        return source
    end

    return nil
end

local SCRIPTS = {
    MM2        = "https://api.jnkie.com/api/v1/luascripts/public/f88bc27f071600baaa1afc246ffb6c53461c215a7db93c969959072152943cd5/download",
    DOORS      = "https://api.jnkie.com/api/v1/luascripts/public/7915991c0c868d1938aff55d370c8050e063cbcb8762a95fd405f21b8587ea2c/download",
    TIMEBOMB   = "https://api.jnkie.com/api/v1/luascripts/public/69a06a1de9966f3012fb2bd2cb8d5d2af674dc9125f4d0ba7b4fd323a8dce635/download",
    FORSAKEN   = "https://api.jnkie.com/api/v1/luascripts/public/7c4032d89f36d9fab5ac0076a4802086eebc9d17c223283ea042bc9753ebd2cc/download",
    DEADRAILS  = "https://api.jnkie.com/api/v1/luascripts/public/19ab1970bbdf3b967d63349f52d7967b0e7a39860a4e463f2f4771a165aa543e/download",
    VOLLEYBALL = "https://api.jnkie.com/api/v1/luascripts/public/41bf8158fc125b3d895f332771b5aeaed072c5b8ea16d8002d0878644fa3578f/download",
    NIGHTS99   = "https://api.jnkie.com/api/v1/luascripts/public/1238dbd70c6f460836b85fca2e3311debed55047f9e21b8207de07caf7867d0f/download",
    HUSSVALLEY = "https://api.jnkie.com/api/v1/luascripts/public/fafaa6d66f82d1f8448f07b70e342014c18adc491dda695c13c0547776342f7e/download",
}

local byGameId = {
    [6931042565] = SCRIPTS.VOLLEYBALL,
    [2440500124] = SCRIPTS.DOORS,
}

local byPlaceId = {
    -- Murder Mystery 2
    [142823291] = SCRIPTS.MM2,
    [335132309] = SCRIPTS.MM2,
    [636649648] = SCRIPTS.MM2,
    [80469437126309] = SCRIPTS.MM2,

    -- DOORS
    [6516141723] = SCRIPTS.DOORS,
    [6839171747] = SCRIPTS.DOORS,
    [10549820578] = SCRIPTS.DOORS,
    [12308344607] = SCRIPTS.DOORS,
    [87716067947993] = SCRIPTS.DOORS,
    [110258689672367] = SCRIPTS.DOORS,

    -- Timebomb Duels
    [11379739543] = SCRIPTS.TIMEBOMB,

    -- Forsaken
    [18687417158] = SCRIPTS.FORSAKEN,
    [83645629621104] = SCRIPTS.FORSAKEN,
    [86454545238517] = SCRIPTS.FORSAKEN,
    [94626476208514] = SCRIPTS.FORSAKEN,
    [106560117662077] = SCRIPTS.FORSAKEN,

    -- Dead Rails
    [70876832253163] = SCRIPTS.DEADRAILS,
    [74106709399219] = SCRIPTS.DEADRAILS,
    [96831577561553] = SCRIPTS.DEADRAILS,
    [110282088381749] = SCRIPTS.DEADRAILS,
    [111285651581407] = SCRIPTS.DEADRAILS,
    [116495829188952] = SCRIPTS.DEADRAILS,

    -- Volleyball Legends
    [73956553001240] = SCRIPTS.VOLLEYBALL,
    [74691681039273] = SCRIPTS.VOLLEYBALL,
    [85395484560711] = SCRIPTS.VOLLEYBALL,
    [86789627188240] = SCRIPTS.VOLLEYBALL,
    [96802054849934] = SCRIPTS.VOLLEYBALL,
    [102580589030177] = SCRIPTS.VOLLEYBALL,
    [103521881639626] = SCRIPTS.VOLLEYBALL,
    [109684591839194] = SCRIPTS.VOLLEYBALL,
    [117134837736236] = SCRIPTS.VOLLEYBALL,
    [134314141048307] = SCRIPTS.VOLLEYBALL,

    -- 99 Nights in the Forest
    [79546208627805] = SCRIPTS.NIGHTS99,
    [126509999114328] = SCRIPTS.NIGHTS99,

    -- Huss Valley
    [107535308163741] = SCRIPTS.HUSSVALLEY,
}

local function getScriptUrl()
    local gameId = game.GameId
    while gameId == 0 and game.PlaceId == 0 do
        task.wait()
        gameId = game.GameId
    end
    return byGameId[gameId] or byPlaceId[game.PlaceId]
end

-- Returns the payload source, or nil plus a message for the UI.
local function deliver(key)
    local url = getScriptUrl()
    if not url then
        return nil, ("Unsupported game. PlaceId=%s GameId=%s"):format(tostring(game.PlaceId), tostring(game.GameId))
    end

    status.Text = "Downloading script..."
    for attempt = 1, 3 do
        local source = fetch(url)
        if source then return source end
        task.wait(0.5)
    end

    return nil, "Could not download the script. Check your connection or executor."
end

-- [LOADER] The main thread waits for the key UI, then fetches and compiles the
--  payload. The payload itself runs in task.spawn so the Continue button and
--  the rest of the game thread are not blocked.
local function runLaunch()
    while true do
        while not launchRequest do
            task.wait(0.1)
        end

        local key = launchRequest
        launchRequest = nil

        status.Text = "Loading Synvextia..."
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Loading"

        local started = os.clock()
        local okCall, payload, err = pcall(deliver, key)
        if not okCall then
            payload, err = nil, tostring(payload)
        end

        if not payload then
            -- keep the UI alive so the key can be retried
            accepted = false
            status.Text = tostring(err or "Loader error")
            status.TextColor3 = COL_ERROR
            checkButton.Text = "Check Key"
            warn("[Synvextia] " .. tostring(err))
        else
            print(("[Synvextia] payload: %d bytes in %.1fs"):format(#payload, os.clock() - started))

            local chunk, compileErr = loadstring(payload)
            if not chunk then
                accepted = false
                status.Text = "Loader script failed to compile"
                status.TextColor3 = COL_ERROR
                checkButton.Text = "Check Key"
                warn("[Synvextia] compile error: " .. tostring(compileErr))
            else
                pcall(function() screenGui:Destroy() end)

                -- Let the pulse loop and any click/auto-login thread finish
                -- before spawning the payload thread.
                task.wait(0.3)

                task.spawn(function()
                    local okRun, runErr = pcall(chunk)
                    if okRun then
                        print(("[Synvextia] loader returned after %.1fs"):format(os.clock() - started))
                    else
                        warn(("[Synvextia] loader failed after %.1fs: %s"):format(os.clock() - started, tostring(runErr)))
                    end
                end)
                break
            end
        end
    end
end

local function checkKey(isAuto)
    if accepted then return end
    local key = normalizeKey(keyBox.Text)
    if key == "" then
        if not isAuto then
            status.Text = "Enter a key first"
            status.TextColor3 = COL_ERROR
        end
        return
    end
    -- [NOTE] Local key check.
    if VALID_KEYS[key] then
        accepted = true
        saveKey(key)
        status.Text = isAuto and "Saved key found! Logging in..." or "Key accepted!"
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Success"
        task.wait(0.6)
        launchRequest = key
    else
        status.Text = "Invalid key - join the server for one"
        status.TextColor3 = COL_ERROR
        if isAuto then
            clearSavedKey()
            keyBox.Text = ""
        end
    end
end

joinButton.MouseButton1Click:Connect(function()
    if busy then return end
    busy = true
    local copied = false
    local fns = {}
    if typeof(setclipboard) == "function" then table.insert(fns, setclipboard) end
    if typeof(writeclipboard) == "function" then table.insert(fns, writeclipboard) end
    table.insert(fns, function(t) return GuiService:SetClipboard(t) end)

    for _, fn in ipairs(fns) do
        local ok = pcall(fn, INVITE)
        if ok then copied = true break end
    end
    if not copied then
        keyBox.Text = INVITE
    end
    joinButton.Text = copied and "Copied! Paste in Discord" or "Invite in box - copy it"
    task.wait(1.8)
    joinButton.Text = "Copy Discord Invite"
    busy = false
end)

checkButton.MouseButton1Click:Connect(function() checkKey(false) end)
keyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then checkKey(false) end
end)

local lastAuto = 0
keyBox:GetPropertyChangedSignal("Text"):Connect(function()
    if accepted then return end
    local k = normalizeKey(keyBox.Text)
    if VALID_KEYS[k] and tick() - lastAuto > 1 then
        lastAuto = tick()
        checkKey(false)
    end
end)

task.spawn(function()
    local saved = loadSavedKey()
    if saved ~= "" then
        keyBox.Text = saved
        status.Text = "Saved key found! Logging in..."
        status.TextColor3 = COL_SUBTEXT
        task.wait(0.6)
        if not screenGui.Parent then return end
        checkKey(true)
    end
end)

task.spawn(function()
    while screenGui.Parent do
        local pulse = math.sin(tick() * 2) * 0.5 + 0.5
        joinGradient.Offset = Vector2.new(0, pulse * 0.6 - 0.3)
        RunService.RenderStepped:Wait()
    end
end)

-- The main thread waits for the key UI, then fetches and compiles the payload.
-- The payload runs in task.spawn so it does not block the UI or game thread.
runLaunch()



-- [LOADSTRING #14] - Chunk: nil
--[[
  Synvextia Key System -> per-game loader
  Key: syn2
  Preserves request-first fetch and task.spawn execution.
]]

print("[Synvextia] loader v2 (direct per-game URLs)")

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local GuiService = game:GetService("GuiService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local INVITE = "https://discord.gg/6YQagDhEqy"
local MESSAGE = "Join the server to get your key\nThere is no checkpoints"
local VALID_KEYS = {
    ["syn2"] = true,
}

local KEY_FILE = "synvextia_key.txt"

local function normalizeKey(s)
    return tostring(s or ""):gsub("%s+", "")
end

-- [NOTE] Some builds read getgenv().SCRIPT_KEY; set both names for compatibility.
local function saveKey(key)
    key = normalizeKey(key)
    if key == "" then return end
    pcall(function()
        if writefile then writefile(KEY_FILE, key) end
    end)
    pcall(function()
        getgenv().SCRIPT_KEY = key
        getgenv().SynvextiaKey = key
    end)
    pcall(function()
        _G.SCRIPT_KEY = key
        _G.SynvextiaKey = key
    end)
end

local function loadSavedKey()
    if typeof(isfile) == "function" and typeof(readfile) == "function" then
        local ok, is = pcall(function() return isfile(KEY_FILE) end)
        if ok and is then
            local ok2, contents = pcall(function() return readfile(KEY_FILE) end)
            if ok2 and contents then
                local k = normalizeKey(contents)
                if k ~= "" then return k end
            end
        end
    end
    if typeof(getgenv) == "function" then
        local ok, k = pcall(function() return getgenv().SCRIPT_KEY or getgenv().SynvextiaKey end)
        if ok and k and normalizeKey(k) ~= "" then return normalizeKey(k) end
    end
    if _G.SynvextiaKey and normalizeKey(_G.SynvextiaKey) ~= "" then
        return normalizeKey(_G.SynvextiaKey)
    end
    return ""
end

local function clearSavedKey()
    pcall(function()
        if typeof(delfile) == "function" and typeof(isfile) == "function" then
            if isfile(KEY_FILE) then delfile(KEY_FILE) end
        elseif writefile then
            writefile(KEY_FILE, "")
        end
    end)
    pcall(function() getgenv().SCRIPT_KEY = nil end)
    pcall(function() _G.SynvextiaKey = nil end)
end

local COL_BG_TOP = Color3.fromRGB(24, 25, 32)
local COL_BG_BOTTOM = Color3.fromRGB(12, 12, 17)
local COL_PANEL_TOP = Color3.fromRGB(48, 50, 58)
local COL_PANEL_BOTTOM = Color3.fromRGB(34, 36, 42)
local COL_ACCENT = Color3.fromRGB(88, 101, 242)
local COL_ACCENT_HOVER = Color3.fromRGB(108, 120, 255)
local COL_SUCCESS = Color3.fromRGB(35, 134, 78)
local COL_ERROR = Color3.fromRGB(178, 58, 72)
local COL_TEXT = Color3.fromRGB(245, 246, 250)
local COL_SUBTEXT = Color3.fromRGB(160, 165, 185)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "SynvextiaKeySystem"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 9999
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

local overlay = Instance.new("Frame")
overlay.Name = "Overlay"
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = COL_BG_BOTTOM
overlay.BackgroundTransparency = 1
overlay.BorderSizePixel = 0
overlay.ZIndex = 1
overlay.Parent = screenGui

local backdropGradient = Instance.new("UIGradient")
backdropGradient.Color = ColorSequence.new(COL_BG_TOP, COL_BG_BOTTOM)
backdropGradient.Rotation = 45
backdropGradient.Parent = overlay
TweenService:Create(overlay, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), { BackgroundTransparency = 0.25 }):Play()

local panel = Instance.new("Frame")
panel.Name = "Panel"
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Position = UDim2.fromScale(0.5, 0.5)
panel.Size = UDim2.new(0.9, 0, 0, 420)
panel.BackgroundColor3 = COL_PANEL_BOTTOM
panel.BorderSizePixel = 0
panel.ZIndex = 2
panel.Parent = overlay

local panelSize = Instance.new("UISizeConstraint")
panelSize.MaxSize = Vector2.new(660, 420)
panelSize.MinSize = Vector2.new(300, 420)
panelSize.Parent = panel

local panelGradient = Instance.new("UIGradient")
panelGradient.Color = ColorSequence.new(COL_PANEL_TOP, COL_PANEL_BOTTOM)
panelGradient.Rotation = 90
panelGradient.Parent = panel

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 18)
panelCorner.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Color = Color3.fromRGB(255, 255, 255)
panelStroke.Transparency = 0.85
panelStroke.Thickness = 1.5
panelStroke.Parent = panel

local accent = Instance.new("Frame")
accent.Name = "Accent"
accent.Size = UDim2.new(1, -80, 0, 6)
accent.Position = UDim2.new(0.5, 0, 0, 24)
accent.AnchorPoint = Vector2.new(0.5, 0)
accent.BackgroundColor3 = COL_ACCENT
accent.BorderSizePixel = 0
accent.ZIndex = 3
accent.Parent = panel
Instance.new("UICorner", accent).CornerRadius = UDim.new(1, 0)

local accentGradient = Instance.new("UIGradient")
accentGradient.Color = ColorSequence.new(Color3.fromRGB(120, 130, 255), COL_ACCENT)
accentGradient.Parent = accent

local wordmark = Instance.new("TextLabel")
wordmark.Name = "Wordmark"
wordmark.AnchorPoint = Vector2.new(0.5, 0)
wordmark.Position = UDim2.new(0.5, 0, 0, 44)
wordmark.Size = UDim2.new(1, -40, 0, 18)
wordmark.BackgroundTransparency = 1
wordmark.Text = "S Y N V E X T I A"
wordmark.TextColor3 = COL_ACCENT_HOVER
wordmark.TextSize = 14
wordmark.Font = Enum.Font.GothamBold
wordmark.TextTransparency = 0.25
wordmark.ZIndex = 3
wordmark.Parent = panel

local title = Instance.new("TextLabel")
title.Name = "Title"
title.AnchorPoint = Vector2.new(0.5, 0)
title.Position = UDim2.new(0.5, 0, 0, 70)
title.Size = UDim2.new(1, -50, 0, 40)
title.BackgroundTransparency = 1
title.Text = "Key System"
title.TextColor3 = COL_TEXT
title.TextSize = 30
title.Font = Enum.Font.GothamBold
title.ZIndex = 3
title.Parent = panel

local message = Instance.new("TextLabel")
message.Name = "Message"
message.AnchorPoint = Vector2.new(0.5, 0)
message.Position = UDim2.new(0.5, 0, 0, 108)
message.Size = UDim2.new(1, -50, 0, 52)
message.BackgroundTransparency = 1
message.Text = MESSAGE
message.TextColor3 = COL_SUBTEXT
message.TextWrapped = true
message.TextSize = 16
message.Font = Enum.Font.Gotham
message.TextXAlignment = Enum.TextXAlignment.Center
message.ZIndex = 3
message.Parent = panel

local joinButton = Instance.new("TextButton")
joinButton.Name = "JoinButton"
joinButton.AnchorPoint = Vector2.new(0.5, 0)
joinButton.Position = UDim2.new(0.5, 0, 0, 164)
joinButton.Size = UDim2.new(1, -100, 0, 50)
joinButton.BackgroundColor3 = COL_ACCENT
joinButton.BorderSizePixel = 0
joinButton.Text = "Copy Discord Invite"
joinButton.TextColor3 = Color3.new(1, 1, 1)
joinButton.TextSize = 22
joinButton.Font = Enum.Font.GothamBold
joinButton.AutoButtonColor = false
joinButton.ZIndex = 3
joinButton.Parent = panel
Instance.new("UICorner", joinButton).CornerRadius = UDim.new(0, 14)

local joinGradient = Instance.new("UIGradient")
joinGradient.Color = ColorSequence.new(COL_ACCENT_HOVER, COL_ACCENT)
joinGradient.Rotation = 90
joinGradient.Parent = joinButton

local joinScale = Instance.new("UIScale")
joinScale.Parent = joinButton
joinButton.MouseEnter:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
joinButton.MouseLeave:Connect(function()
    TweenService:Create(joinScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local keyBox = Instance.new("TextBox")
keyBox.Name = "KeyBox"
keyBox.AnchorPoint = Vector2.new(0.5, 0)
keyBox.Position = UDim2.new(0.5, 0, 0, 236)
keyBox.Size = UDim2.new(1, -110, 0, 42)
keyBox.BackgroundColor3 = Color3.fromRGB(20, 21, 26)
keyBox.BackgroundTransparency = 0.25
keyBox.BorderSizePixel = 0
keyBox.ClearTextOnFocus = false
keyBox.Font = Enum.Font.Code
keyBox.PlaceholderText = "Paste your key here..."
keyBox.Text = ""
keyBox.TextColor3 = COL_TEXT
keyBox.PlaceholderColor3 = COL_SUBTEXT
keyBox.TextSize = 16
keyBox.TextXAlignment = Enum.TextXAlignment.Center
keyBox.ZIndex = 3
keyBox.Parent = panel
Instance.new("UICorner", keyBox).CornerRadius = UDim.new(0, 8)

local checkButton = Instance.new("TextButton")
checkButton.Name = "CheckButton"
checkButton.AnchorPoint = Vector2.new(0.5, 0)
checkButton.Position = UDim2.new(0.5, 0, 0, 296)
checkButton.Size = UDim2.new(1, -100, 0, 50)
checkButton.BackgroundColor3 = COL_SUCCESS
checkButton.BorderSizePixel = 0
checkButton.Text = "Check Key"
checkButton.TextColor3 = Color3.new(1, 1, 1)
checkButton.TextSize = 22
checkButton.Font = Enum.Font.GothamBold
checkButton.AutoButtonColor = false
checkButton.ZIndex = 3
checkButton.Parent = panel
Instance.new("UICorner", checkButton).CornerRadius = UDim.new(0, 14)

local checkScale = Instance.new("UIScale")
checkScale.Parent = checkButton
checkButton.MouseEnter:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1.04 }):Play()
end)
checkButton.MouseLeave:Connect(function()
    TweenService:Create(checkScale, TweenInfo.new(0.12), { Scale = 1 }):Play()
end)

local status = Instance.new("TextLabel")
status.Name = "Status"
status.AnchorPoint = Vector2.new(0.5, 0)
status.Position = UDim2.new(0.5, 0, 0, 360)
status.Size = UDim2.new(1, -40, 0, 20)
status.BackgroundTransparency = 1
status.Text = ""
status.TextColor3 = COL_SUBTEXT
status.TextSize = 14
status.Font = Enum.Font.Gotham
status.ZIndex = 3
status.Parent = panel

local busy = false
local accepted = false
local launchRequest = nil

-- [LOADER] Request-first fetch, then game:HttpGet fallback.
local function fetch(url)
    local req = (type(syn) == "table" and syn.request) or request or http_request
    if type(req) == "function" then
        local ok, res = pcall(req, { Url = url, Method = "GET" })
        if ok and type(res) == "table" and tonumber(res.StatusCode) == 200 and type(res.Body) == "string" and res.Body ~= "" then
            return res.Body
        end
    end

    local ok, source = pcall(game.HttpGet, game, url)
    if ok and type(source) == "string" and source ~= "" then
        return source
    end

    return nil
end

local SCRIPTS = {
    MM2        = "https://api.jnkie.com/api/v1/luascripts/public/f88bc27f071600baaa1afc246ffb6c53461c215a7db93c969959072152943cd5/download",
    DOORS      = "https://api.jnkie.com/api/v1/luascripts/public/7915991c0c868d1938aff55d370c8050e063cbcb8762a95fd405f21b8587ea2c/download",
    TIMEBOMB   = "https://api.jnkie.com/api/v1/luascripts/public/69a06a1de9966f3012fb2bd2cb8d5d2af674dc9125f4d0ba7b4fd323a8dce635/download",
    FORSAKEN   = "https://api.jnkie.com/api/v1/luascripts/public/7c4032d89f36d9fab5ac0076a4802086eebc9d17c223283ea042bc9753ebd2cc/download",
    DEADRAILS  = "https://api.jnkie.com/api/v1/luascripts/public/19ab1970bbdf3b967d63349f52d7967b0e7a39860a4e463f2f4771a165aa543e/download",
    VOLLEYBALL = "https://api.jnkie.com/api/v1/luascripts/public/41bf8158fc125b3d895f332771b5aeaed072c5b8ea16d8002d0878644fa3578f/download",
    NIGHTS99   = "https://api.jnkie.com/api/v1/luascripts/public/1238dbd70c6f460836b85fca2e3311debed55047f9e21b8207de07caf7867d0f/download",
    HUSSVALLEY = "https://api.jnkie.com/api/v1/luascripts/public/fafaa6d66f82d1f8448f07b70e342014c18adc491dda695c13c0547776342f7e/download",
}

local byGameId = {
    [6931042565] = SCRIPTS.VOLLEYBALL,
    [2440500124] = SCRIPTS.DOORS,
}

local byPlaceId = {
    -- Murder Mystery 2
    [142823291] = SCRIPTS.MM2,
    [335132309] = SCRIPTS.MM2,
    [636649648] = SCRIPTS.MM2,
    [80469437126309] = SCRIPTS.MM2,

    -- DOORS
    [6516141723] = SCRIPTS.DOORS,
    [6839171747] = SCRIPTS.DOORS,
    [10549820578] = SCRIPTS.DOORS,
    [12308344607] = SCRIPTS.DOORS,
    [87716067947993] = SCRIPTS.DOORS,
    [110258689672367] = SCRIPTS.DOORS,

    -- Timebomb Duels
    [11379739543] = SCRIPTS.TIMEBOMB,

    -- Forsaken
    [18687417158] = SCRIPTS.FORSAKEN,
    [83645629621104] = SCRIPTS.FORSAKEN,
    [86454545238517] = SCRIPTS.FORSAKEN,
    [94626476208514] = SCRIPTS.FORSAKEN,
    [106560117662077] = SCRIPTS.FORSAKEN,

    -- Dead Rails
    [70876832253163] = SCRIPTS.DEADRAILS,
    [74106709399219] = SCRIPTS.DEADRAILS,
    [96831577561553] = SCRIPTS.DEADRAILS,
    [110282088381749] = SCRIPTS.DEADRAILS,
    [111285651581407] = SCRIPTS.DEADRAILS,
    [116495829188952] = SCRIPTS.DEADRAILS,

    -- Volleyball Legends
    [73956553001240] = SCRIPTS.VOLLEYBALL,
    [74691681039273] = SCRIPTS.VOLLEYBALL,
    [85395484560711] = SCRIPTS.VOLLEYBALL,
    [86789627188240] = SCRIPTS.VOLLEYBALL,
    [96802054849934] = SCRIPTS.VOLLEYBALL,
    [102580589030177] = SCRIPTS.VOLLEYBALL,
    [103521881639626] = SCRIPTS.VOLLEYBALL,
    [109684591839194] = SCRIPTS.VOLLEYBALL,
    [117134837736236] = SCRIPTS.VOLLEYBALL,
    [134314141048307] = SCRIPTS.VOLLEYBALL,

    -- 99 Nights in the Forest
    [79546208627805] = SCRIPTS.NIGHTS99,
    [126509999114328] = SCRIPTS.NIGHTS99,

    -- Huss Valley
    [107535308163741] = SCRIPTS.HUSSVALLEY,
}

local function getScriptUrl()
    local gameId = game.GameId
    while gameId == 0 and game.PlaceId == 0 do
        task.wait()
        gameId = game.GameId
    end
    return byGameId[gameId] or byPlaceId[game.PlaceId]
end

-- Returns the payload source, or nil plus a message for the UI.
local function deliver(key)
    local url = getScriptUrl()
    if not url then
        return nil, ("Unsupported game. PlaceId=%s GameId=%s"):format(tostring(game.PlaceId), tostring(game.GameId))
    end

    status.Text = "Downloading script..."
    for attempt = 1, 3 do
        local source = fetch(url)
        if source then return source end
        task.wait(0.5)
    end

    return nil, "Could not download the script. Check your connection or executor."
end

-- [LOADER] The main thread waits for the key UI, then fetches and compiles the
--  payload. The payload itself runs in task.spawn so the Continue button and
--  the rest of the game thread are not blocked.
local function runLaunch()
    while true do
        while not launchRequest do
            task.wait(0.1)
        end

        local key = launchRequest
        launchRequest = nil

        status.Text = "Loading Synvextia..."
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Loading"

        local started = os.clock()
        local okCall, payload, err = pcall(deliver, key)
        if not okCall then
            payload, err = nil, tostring(payload)
        end

        if not payload then
            -- keep the UI alive so the key can be retried
            accepted = false
            status.Text = tostring(err or "Loader error")
            status.TextColor3 = COL_ERROR
            checkButton.Text = "Check Key"
            warn("[Synvextia] " .. tostring(err))
        else
            print(("[Synvextia] payload: %d bytes in %.1fs"):format(#payload, os.clock() - started))

            local chunk, compileErr = loadstring(payload)
            if not chunk then
                accepted = false
                status.Text = "Loader script failed to compile"
                status.TextColor3 = COL_ERROR
                checkButton.Text = "Check Key"
                warn("[Synvextia] compile error: " .. tostring(compileErr))
            else
                pcall(function() screenGui:Destroy() end)

                -- Let the pulse loop and any click/auto-login thread finish
                -- before spawning the payload thread.
                task.wait(0.3)

                task.spawn(function()
                    local okRun, runErr = pcall(chunk)
                    if okRun then
                        print(("[Synvextia] loader returned after %.1fs"):format(os.clock() - started))
                    else
                        warn(("[Synvextia] loader failed after %.1fs: %s"):format(os.clock() - started, tostring(runErr)))
                    end
                end)
                break
            end
        end
    end
end

local function checkKey(isAuto)
    if accepted then return end
    local key = normalizeKey(keyBox.Text)
    if key == "" then
        if not isAuto then
            status.Text = "Enter a key first"
            status.TextColor3 = COL_ERROR
        end
        return
    end
    -- [NOTE] Local key check.
    if VALID_KEYS[key] then
        accepted = true
        saveKey(key)
        status.Text = isAuto and "Saved key found! Logging in..." or "Key accepted!"
        status.TextColor3 = COL_SUCCESS
        checkButton.Text = "Success"
        task.wait(0.6)
        launchRequest = key
    else
        status.Text = "Invalid key - join the server for one"
        status.TextColor3 = COL_ERROR
        if isAuto then
            clearSavedKey()
            keyBox.Text = ""
        end
    end
end

joinButton.MouseButton1Click:Connect(function()
    if busy then return end
    busy = true
    local copied = false
    local fns = {}
    if typeof(setclipboard) == "function" then table.insert(fns, setclipboard) end
    if typeof(writeclipboard) == "function" then table.insert(fns, writeclipboard) end
    table.insert(fns, function(t) return GuiService:SetClipboard(t) end)

    for _, fn in ipairs(fns) do
        local ok = pcall(fn, INVITE)
        if ok then copied = true break end
    end
    if not copied then
        keyBox.Text = INVITE
    end
    joinButton.Text = copied and "Copied! Paste in Discord" or "Invite in box - copy it"
    task.wait(1.8)
    joinButton.Text = "Copy Discord Invite"
    busy = false
end)

checkButton.MouseButton1Click:Connect(function() checkKey(false) end)
keyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then checkKey(false) end
end)

local lastAuto = 0
keyBox:GetPropertyChangedSignal("Text"):Connect(function()
    if accepted then return end
    local k = normalizeKey(keyBox.Text)
    if VALID_KEYS[k] and tick() - lastAuto > 1 then
        lastAuto = tick()
        checkKey(false)
    end
end)

task.spawn(function()
    local saved = loadSavedKey()
    if saved ~= "" then
        keyBox.Text = saved
        status.Text = "Saved key found! Logging in..."
        status.TextColor3 = COL_SUBTEXT
        task.wait(0.6)
        if not screenGui.Parent then return end
        checkKey(true)
    end
end)

task.spawn(function()
    while screenGui.Parent do
        local pulse = math.sin(tick() * 2) * 0.5 + 0.5
        joinGradient.Offset = Vector2.new(0, pulse * 0.6 - 0.3)
        RunService.RenderStepped:Wait()
    end
end)

-- The main thread waits for the key UI, then fetches and compiles the payload.
-- The payload runs in task.spawn so it does not block the UI or game thread.
runLaunch()
