# Hogyan futtassunk python scriptet a Raspberry Pi indításakor
# _How to run a python script on Raspberry Pi at startup_

Több módja is van, hogy hogyan indítsunk python scriptet induláskor, azonban bármilyen ilyen jellegű művelet kifejezetten **veszélyes**, így előtte mindenképp készítsünk biztonsági mentést.

Az egyik ilyen mód az `/etc/profile` fájl szerkesztése. Szöveget például a `nano` (terminálban működő, majdnem minden linux distron létező egyszerű szövegszerkesztő), a `leafpad` (a Raspbian default szövegszerkesztője) vagy `pluma` (a `gedit`-hez hasnoló, Ubuntu Mate default szövegszerkesztője) segítségével szerkeszthetünk.

```python
sudo nano /etc/profile
sudo pluma /etc/profile
sudo leafpad /etc/profile
```

Tegyük fel, hogy a `/home/pi/futtatni.py` tartalmazza a futtatandó scritünket. Bizonyosodjunk meg róla, hogy a megfelelő futtatási jogok be vannak állítva.

```python
chmod 777 /home/pi/futtatni.py
```

Továbbá bizonyosodjunk meg róla, hogy a `futtatni.py` első sora:
```python
#!/usr/bin/env python
```

Amennyiben ezek rendelkezésre állnak szúrjunk be `/etc/profile` fájl végére:
```python
sudo python3 /home/pi/futtatni.py &
```
**Fontos**: a parancs végén szerepeltessük `&`-t, így a háttérben indul a scriptünk, és ha például végtelen ciklusba kerülne, akkor nem akadályozza az indulást. Több package használata **nem ajánlott**, mint pl. a `pygame`, a `matplotlib` vagy a `pyqt` vagy bármely GUI-t használó csomag.

## Hibaelhárítás 
## _Troubleshoot_
Másik linuxos gépen mountoljuk fel a Raspberry Pi SD kártyáját, így módosíthatjuk a fájlokat, pl. kikommentlehetjük a `futtatni.py` teljes tartalmát.
