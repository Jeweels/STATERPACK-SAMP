# STATERPACK-SAMP

Nama script :  starterpack
```
#include <a_samp>
#include <zcmd>
#include <dini>

enum ClaimStarterPack
{
    Starterpack,
};
new InfoClaimSP[playerid][ClaimStarterPack];

stock GetName(playerid)
{
    new namanya[MAX_PLAYER_NAME];
    GetPlayerName(playerid, namanya, sizeof(namanya));
    return namanya;
}

public OnPlayerConnect(playerid)
{
    new file[128];
    format(file, sizeof file, "ClaimSP/Player-%s.txt", GetName(playerid));
    if(dini_Exists(file))
    {
        InfoClaimSP[playerid][Starterpack] = dini_Int(file, "StarterPackInfo");
    }
    else
    {
        dini_Create(file);
        dini_IntSet(file, "StarterPackInfo", 0);
        InfoClaimSP[playerid][Starterpack] = dini_Int(file, "StarterPackInfo");
    }
    return 1;
}

CMD:claimstarterpack(playerid, params[])
{
    new file[128];
    if(InfoClaimSP[playerid][Starterpack] == 1) return SendClientMessage(playerid, -1, "{ff0000}ERROR: {ffffff}Amda sebelumnya sudah claim Starterpack anda!");
    InfoClaimSP[playerid][Starterpack] = 1;
    format(file, sizeof file, "ClaimSP/Player-%s.txt", GetName(playerid));
    if(dini_Exists(file))
    {
        dini_IntSet(file, "StarterPackInfo", InfoClaimSP[playerid][Starterpack]);
    }
    GivePlayerMoney(playerid, 10000000);
    SendClientMessage(playerid, -1, "{00ff00}INFO: {ffffff}Anda berhasil mengklaim starterpack anda!");
    return 1;
}
NOTE: Buat folder di scriptfiles dengan nama: ClaimSP```
