```lua
local canLoopKill = true
local selected = {}

local plr = owner

plr.Chatted:Connect(function(msg)
	if string.sub(msg, 0, string.len("#Select")) == "#Select" then
		local itemToSearch = msg:gsub("#Select ", "")
		for _, items in next, workspace:GetDescendants() do
			if items.Name == itemToSearch then
				table.insert(selected, items)
				local sb = Instance.new("SelectionBox", items)
				sb.Name = "mamagoatreal_sb"
				sb.Adornee = items
			end
		end
	end
	if string.sub(msg, 0, string.len("#Select Class")) == "#Select Class" then
		local classToSearch = msg:gsub("#Select Class ", "")
		for _, items in next, workspace:GetDescendants() do
			if items.ClassName == classToSearch then
				table.insert(selected, items)
				local sb = Instance.new("SelectionBox", items)
				sb.Name = "mamagoatreal_sb"
				sb.Adornee = items
			end
		end
	end
	if string.sub(msg, 0, string.len("#Select By Text")) == "#Select By Text" then
		local textToSearch = msg:gsub("#Select By Text ", "")
		for _, items in next, workspace:GetDescendants() do
			if items:IsA("TextLabel") or items:IsA("TextButton") and items.Text == textToSearch then
				table.insert(selected, items)
			end
		end
	end
	if string.sub(msg, 0, string.len("#Select By Material")) == "#Select By Material" then
		local materialToSearch = msg:gsub("#Select By Material ", "")
		for _, items in next, workspace:GetDescendants() do
			if items:IsA("BasePart") and items.Material == Enum.Material[materialToSearch] then
				table.insert(selected, items)
				local sb = Instance.new("SelectionBox", items)
				sb.Name = "mamagoatreal_sb"
				sb.Adornee = items
			end
		end
	end
	if string.sub(msg, 0, string.len("#Select All")) == "#Select All" then
		local itemToSearch = msg:gsub("#Select ", "")
		for _, items in next, workspace:GetDescendants() do
			if items ~= game.Workspace.Terrain then
				table.insert(selected, items)
				local sb = Instance.new("SelectionBox", items)
				sb.Name = "mamagoatreal_sb"
				sb.Adornee = items
			end
		end
	end
	if string.sub(msg, 0, string.len("#Unselect")) == "#Unselect" then
		for _, selectedItems in next, selected do
			if selectedItems:FindFirstChild("mamagoatreal_sb") then
				selectedItems:FindFirstChild("mamagoatreal_sb"):Destroy()
			end
		end
		table.clear(selected)
	end
	if string.sub(msg, 0, string.len("#Delete Selected")) == "#Delete Selected" then
		for _, selectedItems in next, selected do
			selectedItems:Destroy()
		end
	end
	if msg == "#Print Selected" then
		for _, items in next, selected do
			print(items)
		end
	end
	if string.sub(msg, 0, string.len("#RunS")) == "#RunS" then
		local CodeToRun = msg:gsub("#RunS ", "")
		loadstring(CodeToRun)()
	end
	if string.sub(msg, 0, string.len("#Print Class")) == "#Print Class" then
		local classToPrint = msg:gsub("#Print Class ", "")
		for _, items in next, workspace:GetDescendants() do
			if items:IsA(classToPrint) then
				print(items.Name)
			end
		end
	end
	if msg == "#Print All" then
		for _, items in next, workspace:GetDescendants() do
			print(items.Name)
		end
	end
	if string.sub(msg, 0, string.len("#Kill")) == "#Kill" then
		local plrToKill = msg:gsub("#Kill ", "")
		for _, items in next, workspace:GetDescendants() do
			if items:IsA("Model") and items:FindFirstChildOfClass("Humanoid") and items.Name == plrToKill then
				items:FindFirstChildOfClass("Humanoid").Health = 0
			end
		end
	end
	if string.sub(msg, 0, string.len("#LoopKill")) == "#LoopKill" then
		local plrToKill = msg:gsub("#LoopKill ", "")
		coroutine.wrap(function()
			while wait() do
				if canLoopKill then
					for _, items in next, workspace:GetDescendants() do
						if items:IsA("Model") and items:FindFirstChildOfClass("Humanoid") and items.Name == plrToKill then
							items:FindFirstChildOfClass("Humanoid").Health = 0
						end
					end
				end
			end
		end)()
	end
	if msg == "#UnLoopKill" then
		canLoopKill = false
	end
	if msg == "#Reload Avatar" then
		owner:LoadCharacter()
	end
end)
```
