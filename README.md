# lj-inventory with QBCore exports and decay
BEWARE THIS IS A CHANGE TO MAKE THE LJ-INVENTORY WORK WITH THE LATEST VERSION OF QBCORE AND THEIR EXPORTS
I DID NOT CREATE THIS SCRIPT, CREDITS FOR THIS SCRIPT GO TO PROJECT SLOTH, LJ

Change all occurances of qb-inventory to lj-inventory inside qb-core


Change giveStarterItems function inside qb-multicharacter and qb-cityhal to this function

```local function giveStarterItems()
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
end```

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
