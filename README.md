# PyPlanet-rankings
This repository contains a MySQL-dependant TrackMania rankings app for PyPlanet, based on the ranking calculations in RASP (former (X)Aseco plugin).

## Installation
* ``cd pyplanet/apps``
* ``git clone https://github.com/TheMaximum/PyPlanet-rankings.git rankings``
* Edit ``pyplanet/settings/apps.py``:
  * Add ``'apps.rankings'`` as new line in the file

## Plugin commands
* `/rank` - shows the current server rank;
* `/nextrank` - shows the next ranked player and the difference in "rankpoints" (difference in local record rank);
* `/topranks` - shows the top ranked players in a list;
* `/norank` - shows the maps on which the player has local record.

## Plugin settings
* `minimum_records_required` (default: `5`) - minimum amount of local records required to get a server rank;
* `rank_chat_announce` (default: `True`) - whether to display the player rank in the chat on every map start;
* `topranks_limit` (default: `100`) - limit of top ranking players to display in the `/topranks` list.

## Rank calculation
The server rank for a player is calculated by determining the average local record rank on the server.
If the player has no (ranked) local record on a map, the maximum local record rank (determined by the `record_limit` setting in the local records app) is used for this map.

Calculation for the player average: ``(({sum of ranks}) + ({maximum} * {unranked maps})) / {total maps on server}``

### Rank example
The server contains `10` maps. The maximum local record to obtain is `100`.
The player is ranked `1` on **three** maps, `10` on **two** maps and has `no record` on the remaining **five** maps.

The average for the player is calculated as: ``((1 + 1 + 1 + 10 + 10) + (100 * 5)) / 10`` = `52.3`.
