# Jumper - Jordi Timmers - s130290

## Omgeving maken

De omgeving is een plain met muren (voor de sierraad), aan de achterkant van de plain staat een rode balk (meer info hierover later). De agent is een vierkantje simpel vierkantje

## Scripts

Er zijn 3 scripts die je moet maken.

### Script 1 - Spawner

Dit script staat op de plane (vloer), omdat de objecten hier worden op gespawned

Het spawner script zal er voor zorgen dat er goede (groene) of slechte (rode) obstakels worden gemaakt. Deze worden gespawned na een random aantal tijd die je kan instellen met de min en max parameter.

Of het obstakel goed of slecht is wordt bepaald door een random bool (50% kans) op goed of slecht. Als het obstakel goed is krijgt het object een andere Tag. Je agent zal dus later naar de tag van het object moeten kijken om te bepalen of hij het moet oppakken (er tegen botsen) of er over moet springen.

### Script 2 - Obstacle

Dit script staat op de obstacels zelf (Maak dus een prefab voor de obstacels)

Het obstacle script zorgt er gewoon voor dat elk obstakel vooruit beweegt met een instelbare snelheid (float MoveSpeed) 

Er is ook een OnCollisionEnter() functie in dit script. Hij kijkt na of hij tegen de agent OF de muur achteraan botst. Als dit waar is dan Destroy()'t hij zichzelf

### Script 3 - AgentScript

Dit script staat op de agent

AgentScript heeft 1 instelbare parameter (float force). Deze parameter bepaald hoe hard de agent springt als hij beslist om te springen.

In de initialize functie (override) zal het script de rigidbody opvragen van de agent en de Z en X as freezen aangezien deze nooit mogen bewegen. Ook wordt in deze functie de originele positie bijgehouden zodat hij gereset kan worden naar deze positie als een episode gedaan is

De OnEpisodeBegin functie (override) reset simpelweg de agent

De heuristic functie (override) stelt simpelweg in dat als je op de spatiebalk drukt in heuristic mode, het mannetje zal springen.

Er is ook een OnCollisionEnter function. Het script kijkt dan tegen wat er gebotst wordt (doormiddel van layers), aan de hand van wat dit object is zal hij een reward toevoegen (positief of negatief) en het object al dan niet verwijderen en de episode stoppen.

Er is ook een OnTriggerEnter function. Deze is gemaakt om te kijken of de agent over de slechte obstakels is gesprongen. Er is een invisible muur gemaakt als trigger achter de barrel om te kijken of de agent er over is. Met als uitkomst een reward uiteraard.

