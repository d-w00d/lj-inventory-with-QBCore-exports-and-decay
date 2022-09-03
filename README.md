# lj-inventory with QBCore exports and decay
BEWARE THIS IS A CHANGE TO MAKE THE LJ-INVENTORY WORK WITH THE LATEST VERSION OF QBCORE AND THEIR EXPORTS
I DID NOT CREATE THIS SCRIPT, CREDITS FOR THIS SCRIPT GO TO PROJECT SLOTH, LJ

Change all occurances of qb-inventory to lj-inventory inside qb-core


Change giveStarterItems function inside qb-multicharacter and qb-cityhal to this function

```lua
local function giveStarterItems()
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    for _, v in pairs(QBCore.Shared.StarterItems) do
        local info = {}
        if v.item == "id_card" then
            info.citizenid = Player.PlayerData.citizenid
            info.firstname = Player.PlayerData.charinfo.firstname
            info.lastname = Player.PlayerData.charinfo.lastname
            info.birthdate = Player.PlayerData.charinfo.birthdate
            info.gender = Player.PlayerData.charinfo.gender
            info.nationality = Player.PlayerData.charinfo.nationality
        elseif v.item == "driver_license" then
            info.firstname = Player.PlayerData.charinfo.firstname
            info.lastname = Player.PlayerData.charinfo.lastname
            info.birthdate = Player.PlayerData.charinfo.birthdate
            info.type = "Class C Driver License"
        end
        exports['lj-inventory']:AddItem(src, v.item, 1, nil, info)
    end
end
```

Then change in all your scripts, the following functions and triggers with their corresponding exports

```lua
Change the QBCore:Server:RemoveItem trigger
to
exports['lj-inventory']:RemoveItem(source, name of item, amount, slot(optional))

Change the QBCore:Server:AddItem trigger to
exports['lj-inventory]:AddItem(source, name of item, amount, slot, info)

Change
QBCore.Functions.TriggerCallback('QBCore:HasItem', function(result)
        if hasitem then
              -- Has Item
        end
end, "sandwich")

To

if QBCore.Functions.HasItem("sandwich") then
        -- Has Item
end

Change QBCore.Functions.GetItemByName(item)
To
exports['lj-inventory]:GetItemByName(source, item)

Change QBCore.Functions.GetItemsByName(item)
to
exports['lj-inventory]:GetItemsByName(source, item)

Change QBCore.Functions.ClearInventory()
to
exports['lj-inventory]:ClearInventory(source, filterItems)

Change QBCore.Functions.SetInventory(items, dontUpdateChat)
to
exports['lj-inventory]:SetInventory(source, items)
```

# Inventory Decay

![image](https://user-images.githubusercontent.com/80186604/163069477-114e14ec-bec1-4f93-8421-42017c605f15.png)

## Credits:
>### aj - aj-inventory
>### loljoshie - lj-inventory
>### qbcore - qb-inventory

## Installation

you need to add a decay and created value in your qb-core/shared/items for all items, the decay is set to be the days the item lasts


```lua
["created"] = nil
["decay"] = 28.0 -- for 28 days
```

