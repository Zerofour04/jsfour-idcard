<h1 align="center"> 👮esx_policeBadge</h1>

## ℹ️Information
- Hey, I reuploaded this resource here. It was removed from the forum because it is not allowed to fork on the forum.
- And I used this script, which was pretty good and free

## 🖼️Pictures
![Preview](https://user-images.githubusercontent.com/60815764/149531284-6eaf11fe-6855-40a1-8ff6-560aa371d4cf.png)
![policebadge](https://github.com/Zerofour04/esx_PoliceBadge/assets/60815764/1d2160bb-cebe-4d2a-96f2-505ffb757335)

## 🧱Requirements
 - [esx_policejob](https://github.com/Zerofour04/esx_policejob-improved) 

## 📋Installation
1. Download the repository
2. Extract it
3. Put it in the `/resource` folder
4. Insert SQL files into your database
5. Add ```start esx_policeBadge``` to your server.cfg
6. Open client/main.lua in esx_policejob and paste this code:
```
 function openMenu()
  ESX.UI.Menu.Open(
	'default', GetCurrentResourceName(), 'id_card_menu',
	{
	    css = 'documenti',
		title    = 'Police Badge',
		elements = {
			{label = 'Check your ID', value = 'checkBadge'},
			{label = 'Show your ID', value = 'showBadge'},
		}
	},
	
	function(data, menu)
		local val = data.current.value

		
		if val == 'checkBadge' then
			TriggerServerEvent('policebadge:open', GetPlayerServerId(PlayerId()), GetPlayerServerId(PlayerId()))
                   local lPed = GetPlayerPed(-1)         
		else
			local player, distance = ESX.Game.GetClosestPlayer()
			
			if distance ~= -1 and distance <= 3.0 then
				if val == 'showBadge' then
				TriggerServerEvent('policebadge:open', GetPlayerServerId(PlayerId()), GetPlayerServerId(player))

				end
			else
			  ESX.ShowNotification('No players nearby')
			end
		
		end
	end,
	function(data, menu)
		menu.close()
	end
)
end
 
 CreateThread(function()
    while true do 
        Citizen.Wait(0)
		if IsControlJustReleased(0, 161) and not isDead and ESX.PlayerData.job and ESX.PlayerData.job.name == 'police' and not ESX.UI.Menu.IsOpen('default', GetCurrentResourceName(), 'id_card_menu') then
			openMenu()
		end
	end
end)
		
CreateThread(function()
    while true do 
        Citizen.Wait(5000)
			if ESX.PlayerData.job and ESX.PlayerData.job.name == 'police' then
            TriggerServerEvent('policebadge:ItemsBadge', GetPlayerPed(-1))
		end	
    end
end)
```

## ⭐Credits
- [Creator](https://github.com/jonassvensson4)
- [Editor](https://forum.cfx.re/u/xenzoc94x/summary)
