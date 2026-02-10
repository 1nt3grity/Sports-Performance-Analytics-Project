 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "25cd5132-9013-46c3-960e-da70394ef1d4",
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "from datascience import *\n",
    "\n",
    "%matplotlib inline\n",
    "import matplotlib.pyplot as plots\n",
    "plots.style.use('fivethirtyeight')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "acf1c9dc-6f9f-440d-a08d-6111359a2dea",
   "metadata": {},
   "outputs": [],
   "source": [
    "playerstats = Table.read_table(\"overall_player_stats.csv\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "dc23c43c-bfe3-4d10-bd56-cdad2e0b6ff4",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>#</th> <th>Player</th> <th>GP-GS</th> <th>MIN</th> <th>AVG</th> <th>FG-FGA</th> <th>FG%</th> <th>3FG-FGA</th> <th>3FG%</th> <th>FT-FTA</th> <th>FT%</th> <th>OFF</th> <th>DEF</th> <th>TOT</th> <th>REB_AVG</th> <th>PF</th> <th>DQ</th> <th>A</th> <th>TO</th> <th>BLK</th> <th>STL</th> <th>PTS</th> <th>PTS_AVG</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>2   </td> <td>Harris, Nyla      </td> <td>21-17</td> <td>437 </td> <td>20.8</td> <td>89-158</td> <td>0.563</td> <td>1-10   </td> <td>0.1  </td> <td>48-64 </td> <td>0.75 </td> <td>61  </td> <td>75  </td> <td>136 </td> <td>6.5    </td> <td>43  </td> <td>1   </td> <td>21  </td> <td>28  </td> <td>8   </td> <td>23  </td> <td>227 </td> <td>10.8   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>21  </td> <td>Toomey, Ciera     </td> <td>22-22</td> <td>543 </td> <td>24.7</td> <td>95-168</td> <td>0.565</td> <td>14-47  </td> <td>0.298</td> <td>28-41 </td> <td>0.683</td> <td>61  </td> <td>95  </td> <td>156 </td> <td>7.1    </td> <td>48  </td> <td>1   </td> <td>33  </td> <td>30  </td> <td>33  </td> <td>14  </td> <td>232 </td> <td>10.5   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>24  </td> <td>Nivar, Indya      </td> <td>22-22</td> <td>606 </td> <td>27.5</td> <td>91-202</td> <td>0.45 </td> <td>16-52  </td> <td>0.308</td> <td>31-57 </td> <td>0.544</td> <td>32  </td> <td>84  </td> <td>116 </td> <td>5.3    </td> <td>64  </td> <td>2   </td> <td>80  </td> <td>55  </td> <td>13  </td> <td>65  </td> <td>229 </td> <td>10.4   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>17  </td> <td>Aarnisalo, Elina  </td> <td>22-14</td> <td>541 </td> <td>24.6</td> <td>86-173</td> <td>0.497</td> <td>19-53  </td> <td>0.358</td> <td>21-25 </td> <td>0.84 </td> <td>13  </td> <td>50  </td> <td>63  </td> <td>2.9    </td> <td>24  </td> <td>0   </td> <td>52  </td> <td>39  </td> <td>3   </td> <td>23  </td> <td>212 </td> <td>9.6    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>0   </td> <td>Grant, Lanie      </td> <td>20-15</td> <td>565 </td> <td>28.3</td> <td>63-148</td> <td>0.426</td> <td>39-96  </td> <td>0.406</td> <td>24-29 </td> <td>0.828</td> <td>3   </td> <td>30  </td> <td>33  </td> <td>1.7    </td> <td>28  </td> <td>0   </td> <td>48  </td> <td>33  </td> <td>1   </td> <td>15  </td> <td>189 </td> <td>9.5    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>7   </td> <td>Brooks, Nyla      </td> <td>22-0 </td> <td>413 </td> <td>18.8</td> <td>65-174</td> <td>0.374</td> <td>38-102 </td> <td>0.373</td> <td>12-26 </td> <td>0.462</td> <td>7   </td> <td>50  </td> <td>57  </td> <td>2.6    </td> <td>29  </td> <td>0   </td> <td>27  </td> <td>30  </td> <td>6   </td> <td>17  </td> <td>180 </td> <td>8.2    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>10  </td> <td>Kelly, Reniya     </td> <td>21-20</td> <td>510 </td> <td>24.3</td> <td>45-152</td> <td>0.296</td> <td>18-57  </td> <td>0.316</td> <td>24-30 </td> <td>0.8  </td> <td>3   </td> <td>39  </td> <td>42  </td> <td>2      </td> <td>23  </td> <td>0   </td> <td>50  </td> <td>26  </td> <td>2   </td> <td>26  </td> <td>132 </td> <td>6.3    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>3   </td> <td>Henderson, Taliyah</td> <td>21-0 </td> <td>245 </td> <td>11.7</td> <td>39-65 </td> <td>0.6  </td> <td>6-16   </td> <td>0.375</td> <td>13-26 </td> <td>0.5  </td> <td>22  </td> <td>26  </td> <td>48  </td> <td>2.3    </td> <td>29  </td> <td>0   </td> <td>5   </td> <td>11  </td> <td>1   </td> <td>15  </td> <td>97  </td> <td>4.6    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>4   </td> <td>Hull, Laila       </td> <td>17-0 </td> <td>219 </td> <td>12.9</td> <td>25-61 </td> <td>0.41 </td> <td>17-44  </td> <td>0.386</td> <td>6-9   </td> <td>0.667</td> <td>14  </td> <td>20  </td> <td>34  </td> <td>2      </td> <td>23  </td> <td>0   </td> <td>16  </td> <td>10  </td> <td>5   </td> <td>11  </td> <td>73  </td> <td>4.3    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>26  </td> <td>Queiroz, Taissa   </td> <td>12-0 </td> <td>140 </td> <td>11.7</td> <td>19-34 </td> <td>0.559</td> <td>0-6    </td> <td>0    </td> <td>5-8   </td> <td>0.625</td> <td>9   </td> <td>23  </td> <td>32  </td> <td>2.7    </td> <td>15  </td> <td>0   </td> <td>12  </td> <td>12  </td> <td>1   </td> <td>7   </td> <td>43  </td> <td>3.6    </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (4 rows omitted)</p>"
      ],
      "text/plain": [
       "#    | Player             | GP-GS | MIN  | AVG  | FG-FGA | FG%   | 3FG-FGA | 3FG%  | FT-FTA | FT%   | OFF  | DEF  | TOT  | REB_AVG | PF   | DQ   | A    | TO   | BLK  | STL  | PTS  | PTS_AVG\n",
       "2    | Harris, Nyla       | 21-17 | 437  | 20.8 | 89-158 | 0.563 | 1-10    | 0.1   | 48-64  | 0.75  | 61   | 75   | 136  | 6.5     | 43   | 1    | 21   | 28   | 8    | 23   | 227  | 10.8\n",
       "21   | Toomey, Ciera      | 22-22 | 543  | 24.7 | 95-168 | 0.565 | 14-47   | 0.298 | 28-41  | 0.683 | 61   | 95   | 156  | 7.1     | 48   | 1    | 33   | 30   | 33   | 14   | 232  | 10.5\n",
       "24   | Nivar, Indya       | 22-22 | 606  | 27.5 | 91-202 | 0.45  | 16-52   | 0.308 | 31-57  | 0.544 | 32   | 84   | 116  | 5.3     | 64   | 2    | 80   | 55   | 13   | 65   | 229  | 10.4\n",
       "17   | Aarnisalo, Elina   | 22-14 | 541  | 24.6 | 86-173 | 0.497 | 19-53   | 0.358 | 21-25  | 0.84  | 13   | 50   | 63   | 2.9     | 24   | 0    | 52   | 39   | 3    | 23   | 212  | 9.6\n",
       "0    | Grant, Lanie       | 20-15 | 565  | 28.3 | 63-148 | 0.426 | 39-96   | 0.406 | 24-29  | 0.828 | 3    | 30   | 33   | 1.7     | 28   | 0    | 48   | 33   | 1    | 15   | 189  | 9.5\n",
       "7    | Brooks, Nyla       | 22-0  | 413  | 18.8 | 65-174 | 0.374 | 38-102  | 0.373 | 12-26  | 0.462 | 7    | 50   | 57   | 2.6     | 29   | 0    | 27   | 30   | 6    | 17   | 180  | 8.2\n",
       "10   | Kelly, Reniya      | 21-20 | 510  | 24.3 | 45-152 | 0.296 | 18-57   | 0.316 | 24-30  | 0.8   | 3    | 39   | 42   | 2       | 23   | 0    | 50   | 26   | 2    | 26   | 132  | 6.3\n",
       "3    | Henderson, Taliyah | 21-0  | 245  | 11.7 | 39-65  | 0.6   | 6-16    | 0.375 | 13-26  | 0.5   | 22   | 26   | 48   | 2.3     | 29   | 0    | 5    | 11   | 1    | 15   | 97   | 4.6\n",
       "4    | Hull, Laila        | 17-0  | 219  | 12.9 | 25-61  | 0.41  | 17-44   | 0.386 | 6-9    | 0.667 | 14   | 20   | 34   | 2       | 23   | 0    | 16   | 10   | 5    | 11   | 73   | 4.3\n",
       "26   | Queiroz, Taissa    | 12-0  | 140  | 11.7 | 19-34  | 0.559 | 0-6     | 0     | 5-8    | 0.625 | 9    | 23   | 32   | 2.7     | 15   | 0    | 12   | 12   | 1    | 7    | 43   | 3.6\n",
       "... (4 rows omitted)"
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "playerstats"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "5b77b8a4-3ace-489e-a040-e90bc8e64f69",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Player</th> <th>FG%</th> <th>3FG%</th> <th>FT%</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>Harris, Nyla      </td> <td>0.563</td> <td>0.1  </td> <td>0.75 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Toomey, Ciera     </td> <td>0.565</td> <td>0.298</td> <td>0.683</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Nivar, Indya      </td> <td>0.45 </td> <td>0.308</td> <td>0.544</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Aarnisalo, Elina  </td> <td>0.497</td> <td>0.358</td> <td>0.84 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Grant, Lanie      </td> <td>0.426</td> <td>0.406</td> <td>0.828</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Brooks, Nyla      </td> <td>0.374</td> <td>0.373</td> <td>0.462</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Kelly, Reniya     </td> <td>0.296</td> <td>0.316</td> <td>0.8  </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Henderson, Taliyah</td> <td>0.6  </td> <td>0.375</td> <td>0.5  </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Hull, Laila       </td> <td>0.41 </td> <td>0.386</td> <td>0.667</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Queiroz, Taissa   </td> <td>0.559</td> <td>0    </td> <td>0.625</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (4 rows omitted)</p>"
      ],
      "text/plain": [
       "Player             | FG%   | 3FG%  | FT%\n",
       "Harris, Nyla       | 0.563 | 0.1   | 0.75\n",
       "Toomey, Ciera      | 0.565 | 0.298 | 0.683\n",
       "Nivar, Indya       | 0.45  | 0.308 | 0.544\n",
       "Aarnisalo, Elina   | 0.497 | 0.358 | 0.84\n",
       "Grant, Lanie       | 0.426 | 0.406 | 0.828\n",
       "Brooks, Nyla       | 0.374 | 0.373 | 0.462\n",
       "Kelly, Reniya      | 0.296 | 0.316 | 0.8\n",
       "Henderson, Taliyah | 0.6   | 0.375 | 0.5\n",
       "Hull, Laila        | 0.41  | 0.386 | 0.667\n",
       "Queiroz, Taissa    | 0.559 | 0     | 0.625\n",
       "... (4 rows omitted)"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "playerstats.select('Player','FG%','3FG%','FT%')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "50fb23ac-74b6-460f-a3cb-387793409817",
   "metadata": {},
   "outputs": [],
   "source": [
    "playerstats= playerstats.with_column(\n",
    "    'Shotavg',\n",
    "    (playerstats.column('FG%')\n",
    "     + playerstats.column('3FG%')\n",
    "     +playerstats.column('FT%'))/3\n",
    ")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "dc6fd356-75b0-4ea6-9d3f-6bbfd197f7ad",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Player</th> <th>Shotavg</th> <th>MIN</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>Harris, Nyla      </td> <td>0.471   </td> <td>437 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Toomey, Ciera     </td> <td>0.515333</td> <td>543 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Nivar, Indya      </td> <td>0.434   </td> <td>606 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Aarnisalo, Elina  </td> <td>0.565   </td> <td>541 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Grant, Lanie      </td> <td>0.553333</td> <td>565 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Brooks, Nyla      </td> <td>0.403   </td> <td>413 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Kelly, Reniya     </td> <td>0.470667</td> <td>510 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Henderson, Taliyah</td> <td>0.491667</td> <td>245 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Hull, Laila       </td> <td>0.487667</td> <td>219 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Queiroz, Taissa   </td> <td>0.394667</td> <td>140 </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (4 rows omitted)</p>"
      ],
      "text/plain": [
       "Player             | Shotavg  | MIN\n",
       "Harris, Nyla       | 0.471    | 437\n",
       "Toomey, Ciera      | 0.515333 | 543\n",
       "Nivar, Indya       | 0.434    | 606\n",
       "Aarnisalo, Elina   | 0.565    | 541\n",
       "Grant, Lanie       | 0.553333 | 565\n",
       "Brooks, Nyla       | 0.403    | 413\n",
       "Kelly, Reniya      | 0.470667 | 510\n",
       "Henderson, Taliyah | 0.491667 | 245\n",
       "Hull, Laila        | 0.487667 | 219\n",
       "Queiroz, Taissa    | 0.394667 | 140\n",
       "... (4 rows omitted)"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "playerstats.select('Player','Shotavg','MIN')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "4c3142f3-8857-43b2-bcb0-3c7c4f18fcc6",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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A0+fPoWrq6vGl23Z2Njgf//7n8a36xKVJFOnToWxsTHq1q2L0NDQXF+wRkRERFSaFbgYyMzM1PiG3hyWlpbIysoqUlBEQktJSdF1CEREREQ6V+A1A0REREREVDoUamvR58+fY8uWLRrP5bzwauvWrcq959+n6cVORERERERUvAq8taiVlVWRdl0xMDBAcnJyoa8n0hexdx9CJpPrOoxSQS6XIT09A+bmZtxSUIuYV2Ewr8JgXovG2soC9rbqL+YEuLWoUIorrwV+MlC5cmVuwUhUDGpVddJ1CKXGf/9DrcR/qLSIeRUG8yoM5pVIswIXA9euXRMiDiIiIiIiKmZcQExEREREpKdYDBARERER6SkWA0REREREeorFABERERGRnirUewaISHjcWlR73m4pKEXG/cfcUlCLmFdhMK/CYF4L7kPbiVLpwWKAqISauyYCaa/TdR1GqSCXy5CRkQkzM1N+CNAi5lUYzKswmNeCCxrjy2JAD3CaEBERERGRnmIxQERERESkp1gMEBERERHpKRYDRERERER6isUAEREREZGeYjFARERERKSnWAxQsQoPD4dEIkF4eLjKcTc3N7i5uekoqryFhIRAIpHg1KlTKsclEgm8vLx0FBURERFR0bAYIDx48AASiQS9e/fOtc358+chkUjg7+9fjJEVTH7ug4iIiIj+w2KAKB+GDx+Oc+fOoVGjRroOhYiIiEhr+AZionyoUKECKlSooOswiIiIiLSKTwaoSD4019/LywsSiaR4A8qnhIQEzJgxA+3atUPVqlVha2sLNzc3fP/990hKSlJrn9uaAU3u3r2LKVOmwMPDAy4uLrCzs0OjRo0QHByM169fC3E7RERERIXCJwOkl2JiYrB06VJ4eHigUaNGMDIywtWrV7F27Vr8/vvvOHHiBCwtLQvVd2RkJMLCwtCiRQs0b94ccrkcFy5cwIIFC3D69GkcOHAARkZGWr4jIiIiooJjMUBK9+7dQ0hIiMZzT548KeZohOXh4YFbt26hbNmyKse3bNkCf39/rF69GuPHjy9U397e3hg1ahSMjY1VjoeGhiIkJAS7d+9Gnz598uxHIZdBLpcVKgZSJZfLVX4m7WBehcG8CoN5LTi5XIbMzMw822VlZan8TNrxfl5NTU0FGYfFACndv38foaGhug6jWNjY2Gg83rdvXwQGBiIqKqrQxYCDg4PG48OHD0dISAiioqLyVQxkZGYiIyPv/wlT/kml/IdKCMyrMJhXYTCv+ZeenoH4+Ph8t09MTBQwGv2VmJgIsVgMV1dXQfpnMUBKbdu2xa5duzSeO3/+PNq3b1/MEQlr7969WL9+Pa5cuYKUlBTIZP99C//06dNC96tQKLBp0yZs3rwZsbGxSE1NVfkmKr99m5maIvsNv8HSBrlcDqk0CyYmxhCJuFRKW5hXYTCvwmBeC87c3AyOjpXybJeVlYXExETY2dmpPRWnwiuuvLIYIL20ePFiBAUFwdraGm3atIGDg4Py8dvy5cshlUoL3XdAQABWr16NypUrw9PTE/b29sq/xKGhofnu20AkhkgkLnQcpE4kEjGnAmBehcG8CoN5zT+RSFygqSnGxsaCTWXRZ0LnlcUAFYlIJEJ2drbGc6mpqcUcTf68efMGs2fPRsWKFXHq1ClYW1srzykUCixatKjQfSclJWHNmjWoU6cOjh49CnNzc+W5xMREvZmGRURERB8HPiejIpFIJEhKSsKbN29Ujv/777+4d++ejqL6sOTkZKSmpuLTTz9VKQQA4NKlS8jIyCh033FxcVAoFGjVqpVKIQAAZ86cKXS/REREREJgMUBF0qBBA2RnZ2P79u3KYwqFAlOnTsW///5b5P4lEonW31VgY2MDMzMzXLlyBenp6crjKSkpCAgIKFLfjo6OAIBz586prBN4/PgxgoODi9Q3ERERkbZxmhAVyVdffYXw8HB88803iIqKQoUKFXDmzBm8evUKdevWxfXr1wvdt0KhAACIxQWb23njxg34+/trPFe/fn2MGDECQ4cOxZIlS9C8eXN06tQJaWlpOHbsGBwdHVGxYsVCx2xvb49u3bph7969aNWqFVq2bIlnz57h8OHD8PDwQFxcXKH7JiIiItI2FgNUJHXq1MHOnTvx888/Y8+ePShTpgzat2+Pn3/+GYMHDy5S33///TcAoHfv3gW6LiEhAVu2bNF47tWrVxgxYgR++uknWFlZYfPmzVi7di1sbGzQq1cvTJo0CU2aNClS3MuWLYOTkxP27t2LVatWoXLlyhg1ahTGjh2b65amRERERLpgkJKSotB1EESarFq1CoGBgYiJiUGtWrV0HU6xGzZxAdJep+fdkPIkl8uQkZEJMzNT7iKiRcyrMJhXYTCvBRc0xhd1azjn2S4zMxPx8fFwdHTkbkJaVFx55ZoBKrHOnDkDT09PvSwEiIiIiIoDpwlRibVu3Tpdh0BERERUqvHJABERERGRnmIxQERERESkp1gMEBERERHpKRYDRERERER6iguIiUqo74f1gkwmz7sh5UkulyE9PQPm5mbcUlCLmFdhMK/CYF4LztrKQtchUDFgMUBUQtWq6qTrEEqN//ZqrsQ9sLWIeRUG8yoM5pVIM04TIiIiIiLSUywGiIiIiIj0FIsBIiIiIiI9xWKAiIiIiEhPsRggIiIiItJTLAaIiIiIiPQUtxYlKqFi7z7kewa05O3+4lJk3H/M/cW1iHkVBvOqPdZWFrC3La/rMIhKNBYDRCXU3DURSHudruswSgW5XIaMjEyYmZnyw5UWMa/CYF61J2iML4sBojxwmhARERERkZ5iMUBEREREpKdYDBARERER6SkWA0REREREeorFABERERGRnmIxQERERESkp1gMlGIhISGQSCQ4deqUrkMpER48eACJRAJ/f39dh0JERERUIrAY0JKTJ09i8ODBqFOnDmxtbeHi4gJPT0+sXLkSWVlZug7vo+Lv7w+JRJLvH+Hh4boOmYiIiOijxJeOFdGbN28wfvx4rF+/HmXKlEG7du3g6uqK1NRUHD9+HIGBgVi/fj22b98OR0fHYo1t+PDh6N27NypXrlys4xaVl5cXnJycVI7t378f169fh4+Pj9o5Nze3fPXr4OCAc+fOwcLCQmuxEhEREX3MWAwU0dSpU7F+/Xo0bNgQmzZtgoODg/KcTCZDaGgoZs2ahT59+uD48eMwMzMrttgqVKiAChUqFNt42tKlSxd06dJF5djDhw9x/fp1+Pr6okWLFoXq18jICNWrV9dGiERERESlAqcJFcE///yDpUuXwsrKClu3blUpBABALBbjhx9+wJdffonY2FisXLlS5bxEIoGXl5fGvt3c3DR+452VlYUlS5bAw8MDDg4OqFy5Mjw9PXHgwAG1tprWDLw7b/727dvw8/ODq6srJBIJHjx4AODt046lS5eiWbNmsLe3h5OTE7p06YLDhw+rjZHXFB6h1yuEhYXBx8cHbm5usLOzg7OzM3r16oWTJ0+qtc1tzcDTp08RGBiIhg0bwt7eHs7OzmjatCm+//57pKamKtu9evUK06dPx+eff45KlSrByckJn332GUaOHIlHjx4p2yUkJGDGjBlo164d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",
      "text/plain": [
       "<Figure size 600x700 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "playerstats.barh('Player','Shotavg') #list of UNC CHAPEL HILL WBB players"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "5412d414-2659-453f-9a48-e5bf0203ba30",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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u3fvVr9+/a56LgAAagO3w8GWLVv03HPP6auvvrriWJPJpLy8vErNHx8fr/nz5ysjI0NJSUmGfRkZGY4x7vjpp58kqcIPdAIAoDZz66fhpk2bNGzYMJWWlqpu3bqKiYlRo0aNFBDg1uMTDHr37q2WLVtq1apVeuSRR9SpUydJF08nzJs3T0FBQRo1apRjfF5envLy8hQVFaWoqCjH9i1btujWW291+vyHjIwMffzxxwoPD1f37t09VjcAADWVW+EgOTlZpaWlGj58uF566SU1bNjQU3U5BAUFKSUlRUlJSRowYICSkpJkNpuVnp6u48ePa9asWWrbtq1jfGpqqubOnatp06ZpxowZju3333+/oqKi1LVrV1177bU6f/689u/fr61bt6pOnTpauHChQkNDPV4/AAA1jVvhYO/evYqIiNDixYsVGBjoqZqcJCQkaN26dUpOTtaaNWtUWlqqDh066Omnn9aIESMqNMeMGTP0+eefa/v27Tp9+rRMJpOuvfZaPfjggxo/frxiY2OrrH4AAGoSk8ViufTVg1fQsmVLtW7d2nHuH7VXcXGxcnJy1Lx5c69fResr6IkzeuIafXFGT5z5Uk/cujjglltu0YkTJy57dwIAAKhZ3AoH06ZNU0FBgRYuXOipegAAgJdV+JqDnJwcp23XXHON/vznP2vWrFnasWOHxowZo1atWql+/fqXnKd58+ZXVykAAKgWFQ4HnTp1croN0M5ms+mTTz7RJ598ctk5ruY5BwAAoHpVOBxcd911lwwHAACg9qhwONi3b19V1gEAAHyE5x5lCAAAagWPf5jAkSNHtGjRIv373/9WaWmpWrdurQceeEADBgzw9KEAAEAVqNTKQUZGhtq2bauRI0e63J+ZmanevXvr3Xff1TfffKODBw/qk08+0QMPPKBnn33WE/UCAIAqVqlwsHHjRv3888+69957nfaVlJRo/PjxOnfunOrXr6+JEydq/vz5jscbp6SkaMeOHZ6pGgAAVJlKnVbYsWOHTCaTy1MEa9eu1ffff6+AgACtXr1aPXr0kCT9/ve/V0xMjF555RW9++67ju0AAMA3VWrl4IcfflCrVq0UHh7utO+zzz6TJPXq1cspADz22GMKDg7Wl19+6UapAACgOlQqHOTl5alBgwYu9+3cuVMmk0n9+vVz2hcREaHmzZvrxx9/vLoqAQBAtalU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X3+tmTNn6vnnn9eYMWNUVlbm7fKq1b59+/TKK6/o8ccf10033eTtcnzKtGnT1KtXL0VFRclsNuuWW27R+++/r549e+rLL7/Up59+6u0Sq5XVapUkBQcHKy0tTV27dlVYWJhuvfVW/f3vf1dAQIAWLVrk5SorhnAAg/DwcEkX/+XoSmFhoWGc/c+XSquuxvsim82miRMnasWKFRoxYoQWLFhg2O+vfQkMDFSLFi301FNPadasWfr444/197//XZL/9GT8+PFq1aqVpk+fXqHx/tKXSwkICNCoUaMkSTt27JDkPz2x13PTTTepadOmhn2xsbFq2bKljh07JovF4vM9IRzAwH7e6tcXz9jZz2fZx9n/fPbsWeXm5lZovK+xWq167LHH9N5772nYsGFavHixAgKM/2v4Y19+rW/fvpL+c1GUv/Tkm2++0aFDhxQdHW14yM/y5cslSf369VNkZKQ+/vhjSf7Tl8uxX2tw7tw5Sf7Tk3bt2km69KkC+/bi4mKf7wnhAAZt2rRR06ZNtWPHDhUVFRn2FRcXa+vWrWratKnhIpr4+HhJUkZGhtN89m32Mb7GarXq8ccfV1pamoYOHaq//OUvLm8/8re+uPLTTz9J+s+tWP7SkzFjxrj8Zf9L+K677tKYMWMctwr7S18u59///rck+V1P7A8gOnTokNO+0tJSHT16VKGhoWrUqJHP94RwAAOTyaQxY8bo7Nmzevnllw375s+fL4vFojFjxshkMjm2jx49WkFBQXr11VcNS2RZWVn65z//qVatWikhIaHa3kNF2VcM0tLSNGTIEKWmpl7y3nV/6cvevXtdLnOeOXNGc+bMkXTxSnTJf3qycOFCl7+6d+8u6eI96QsXLlSnTp0k+U9fDhw4IIvF4rR927ZteuONN1S3bl3dfffdkvynJ61atVJiYqKOHj2qd99917BvwYIFys/P18CBAxUUFOTzPeEJiX7i3Xff1bZt2yRdvF/766+/VlxcnFq1aiVJGjhwoAYNGiTJ+ZGeN910k7755htt2LDhko/0fOWVV/TCCy84Hul57tw5rV69WufPn9fq1at97n9iSUpOTtbcuXMVFham//qv/3IZDAYOHOj4S98f+jJ9+nQtW7ZMvXr1UkxMjONR259++qnOnj2re+65R3/7298cp138oSeXMn78eC1fvrxCj0+ujX1JTk5WSkqKEhISFBMTo7p16yorK0sZGRkKCAjQggUL9OCDDzrG+0NPJOnYsWO64447dOrUKfXv31/t2rXT3r17tWnTJjVv3lyfffaZ41ZEX+4J4cBP2P8iu5Rp06ZpxowZjq/tt7J99NFHys3NVXR0tO655x5NmzbtkufTVqxYocWLF+vAgQOqU6eOunfvrpkzZ6pr164efz+ecKWeSHJ6xHRt78u2bdu0bNkyffXVV/rpp5907tw5NWjQQJ07d9Z9992npKQkw79kpNrfk0u5XDiQan9fMjMztWTJEn399dc6deqUiouL1aRJE8XFxWnChAm6+eabnV5T23ti9/333+vFF1/U559/rp9//lnR0dG66667NHXqVKdbEX21J4QDAABgwDUHAADAgHAAAAAMCAcAAMCAcAAAAAwIBwAAwIBwAAAADAgHAADAgHAAAAAMCAcAAMCAcAAAAAwIBwDc0rFjR0VGRioyMlJPP/30ZccuXrzYMTYyMtKwb+DAgYqMjFRycrJh++bNmx3j27dvr/Pnz7uc+4cffnA5L4DKIxwA8JhVq1apvLz8kvtXrFjh1vy5ublasmSJW3MAuDLCAQCPaNeunXJzc7Vx40aX+w8fPqzdu3erXbt2VzW//SO1X3/9dZ07d+5qywRQAYQDAB4xYsQISdL777/vcr99+8iRI69q/piYGHXv3l2nTp3S22+/fXVFAqgQwgEAj4iPj9d1112ntWvXqqioyLDPZrNpxYoVqlevnu6+++6rPsaMGTMkXVw9OHv2rFv1Arg0wgEAjzCZTBo+fLiKior08ccfG/Zt27ZNJ06c0MCBAxUWFnbVx+jbt6969uypvLw8paamulsygEsgHADwGPspg1+fWnD3lMIvTZ8+XZK0cOFCFRYWuj0fAGeEAwAe06FDB3Xq1En/+te/9NNPP0mSLly4oP/5n/9R48aN1bdvX7eP0bt3b8XHx+vMmTN666233J4PgDPCAQCPGjlypMrLy7Vq1SpJ0rp165Sfn6+kpCQFBQV55Bj2aw/eeOMN5efne2ROAP9BOADgUcOGDVNgYKDjVIInTynY9erVSwkJCbJYLFq8eLHH5gVwEeEAgEdFR0erT58+2rdvn7Zs2aLPPvtM119/vbp06eLR48ycOVOS9Oabb8pisXh0bsDfEQ4AeJx9leCRRx5RSUmJR1cN7OLi4tS3b18VFBRo0aJFHp8f8GeEAwAeN2jQIIWFhen777933OJYFeyrB3/5y1905syZKjkG4I88c3UQAPxC/fr19eijj2r79u1q06aNYmJiquQ43bp1U79+/bRhwwYtXLiwSo4B+CPCAYAqYb+joDqOs2HDBsfdEQDcx2kFADVa165d1b9//8t+GiSAyiEcAKjxqmuVAvAXJovFYvN2EQAAwHewcgAAAAwIBwAAwIBwAAAADAgHAADAgHAAAAAMCAcAAMCAcAAAAAwIBwAAwIBwAAAADAgHAADAgHAAAAAMCAcAAMCAcAAAAAz+PxEg62zSbZ96AAAAAElFTkSuQmCC",
      "text/plain": [
       "<Figure size 500x500 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "playerstats.scatter('MIN','Shotavg') #this shows the correlation between shooting avg and minutes we know that players some players with low minutes still have great shooting averages"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "6feb8a80-de67-45bc-ab7b-f6ed397af16f",
   "metadata": {},
   "outputs": [],
   "source": [
    "results= Table.read_table('game_results.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "43d5d9c7-07ee-4892-992d-c256fe619b38",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Date</th> <th>Opponent</th> <th>Conference</th> <th>W/L</th> <th>Score</th> <th>Attendance</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>11/03/25</td> <td>N.C. CENTRAL       </td> <td>nan       </td> <td>W   </td> <td>90-42</td> <td>6336      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/06/25</td> <td>ELON               </td> <td>nan       </td> <td>W   </td> <td>71-37</td> <td>3111      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/13/25</td> <td>vs UCLA            </td> <td>nan       </td> <td>L   </td> <td>60-78</td> <td>1588      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/15/25</td> <td>vs Fairfield       </td> <td>nan       </td> <td>W   </td> <td>82-68</td> <td>2116      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/20/25</td> <td>at N.C. A&T        </td> <td>nan       </td> <td>W   </td> <td>85-50</td> <td>0         </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/23/25</td> <td>UNC GREENSBORO     </td> <td>nan       </td> <td>W   </td> <td>94-48</td> <td>2418      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/27/25</td> <td>vs South Dakota St.</td> <td>nan       </td> <td>W   </td> <td>83-48</td> <td>0         </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/28/25</td> <td>vs Kansas St.      </td> <td>nan       </td> <td>W   </td> <td>85-73</td> <td>200       </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/29/25</td> <td>vs Columbia        </td> <td>nan       </td> <td>W   </td> <td>80-63</td> <td>0         </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>12/04/25</td> <td>at Texas           </td> <td>nan       </td> <td>L   </td> <td>64-79</td> <td>9020      </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (12 rows omitted)</p>"
      ],
      "text/plain": [
       "Date     | Opponent            | Conference | W/L  | Score | Attendance\n",
       "11/03/25 | N.C. CENTRAL        | nan        | W    | 90-42 | 6336\n",
       "11/06/25 | ELON                | nan        | W    | 71-37 | 3111\n",
       "11/13/25 | vs UCLA             | nan        | L    | 60-78 | 1588\n",
       "11/15/25 | vs Fairfield        | nan        | W    | 82-68 | 2116\n",
       "11/20/25 | at N.C. A&T         | nan        | W    | 85-50 | 0\n",
       "11/23/25 | UNC GREENSBORO      | nan        | W    | 94-48 | 2418\n",
       "11/27/25 | vs South Dakota St. | nan        | W    | 83-48 | 0\n",
       "11/28/25 | vs Kansas St.       | nan        | W    | 85-73 | 200\n",
       "11/29/25 | vs Columbia         | nan        | W    | 80-63 | 0\n",
       "12/04/25 | at Texas            | nan        | L    | 64-79 | 9020\n",
       "... (12 rows omitted)"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "results"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "4e50128d-f4b3-4a31-8e0a-c91732f8787d",
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "ccc72b14-4af9-459a-90fd-4fb5248f7438",
   "metadata": {},
   "outputs": [],
   "source": [
    "cplayerstats= Table.read_table('conference_player_stats.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "95298261-36a4-465e-918c-780fec47642c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>#</th> <th>Player</th> <th>GP-GS</th> <th>MIN</th> <th>AVG</th> <th>FG-FGA</th> <th>FG%</th> <th>3FG-FGA</th> <th>3FG%</th> <th>FT-FTA</th> <th>FT%</th> <th>OFF</th> <th>DEF</th> <th>TOT</th> <th>REB_AVG</th> <th>PF</th> <th>DQ</th> <th>A</th> <th>TO</th> <th>BLK</th> <th>STL</th> <th>PTS</th> <th>PTS_AVG</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>2   </td> <td>Harris, Nyla      </td> <td>9-9  </td> <td>233 </td> <td>25.9</td> <td>47-81 </td> <td>0.58 </td> <td>1-4    </td> <td>0.25 </td> <td>24-30 </td> <td>0.8  </td> <td>29  </td> <td>41  </td> <td>70  </td> <td>7.8    </td> <td>19  </td> <td>0   </td> <td>11  </td> <td>13  </td> <td>2   </td> <td>17  </td> <td>119 </td> <td>13.2   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>10  </td> <td>Kelly, Reniya     </td> <td>9-8  </td> <td>270 </td> <td>30  </td> <td>32-88 </td> <td>0.364</td> <td>13-33  </td> <td>0.394</td> <td>17-19 </td> <td>0.895</td> <td>2   </td> <td>19  </td> <td>21  </td> <td>2.3    </td> <td>10  </td> <td>0   </td> <td>18  </td> <td>15  </td> <td>1   </td> <td>12  </td> <td>94  </td> <td>10.4   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>0   </td> <td>Grant, Lanie      </td> <td>9-8  </td> <td>271 </td> <td>30.1</td> <td>29-70 </td> <td>0.414</td> <td>19-46  </td> <td>0.413</td> <td>11-13 </td> <td>0.846</td> <td>1   </td> <td>18  </td> <td>19  </td> <td>2.1    </td> <td>17  </td> <td>0   </td> <td>18  </td> <td>17  </td> <td>0   </td> <td>8   </td> <td>88  </td> <td>9.8    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>21  </td> <td>Toomey, Ciera     </td> <td>9-9  </td> <td>235 </td> <td>26.1</td> <td>35-72 </td> <td>0.486</td> <td>7-21   </td> <td>0.333</td> <td>8-13  </td> <td>0.615</td> <td>22  </td> <td>44  </td> <td>66  </td> <td>7.3    </td> <td>20  </td> <td>1   </td> <td>13  </td> <td>10  </td> <td>13  </td> <td>3   </td> <td>85  </td> <td>9.4    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>24  </td> <td>Nivar, Indya      </td> <td>9-9  </td> <td>255 </td> <td>28.3</td> <td>26-75 </td> <td>0.347</td> <td>3-18   </td> <td>0.167</td> <td>11-20 </td> <td>0.55 </td> <td>13  </td> <td>27  </td> <td>40  </td> <td>4.4    </td> <td>25  </td> <td>1   </td> <td>30  </td> <td>31  </td> <td>3   </td> <td>19  </td> <td>66  </td> <td>7.3    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>17  </td> <td>Aarnisalo, Elina  </td> <td>9-2  </td> <td>186 </td> <td>20.7</td> <td>24-54 </td> <td>0.444</td> <td>5-17   </td> <td>0.294</td> <td>7-8   </td> <td>0.875</td> <td>2   </td> <td>18  </td> <td>20  </td> <td>2.2    </td> <td>11  </td> <td>0   </td> <td>18  </td> <td>14  </td> <td>2   </td> <td>6   </td> <td>60  </td> <td>6.7    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>26  </td> <td>Queiroz, Taissa   </td> <td>7-0  </td> <td>75  </td> <td>10.7</td> <td>12-20 </td> <td>0.6  </td> <td>0-5    </td> <td>0    </td> <td>4-4   </td> <td>1    </td> <td>4   </td> <td>12  </td> <td>16  </td> <td>2.3    </td> <td>10  </td> <td>0   </td> <td>5   </td> <td>6   </td> <td>1   </td> <td>3   </td> <td>28  </td> <td>4      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>7   </td> <td>Brooks, Nyla      </td> <td>9-0  </td> <td>151 </td> <td>16.8</td> <td>11-48 </td> <td>0.229</td> <td>5-29   </td> <td>0.172</td> <td>7-9   </td> <td>0.778</td> <td>2   </td> <td>18  </td> <td>20  </td> <td>2.2    </td> <td>5   </td> <td>0   </td> <td>12  </td> <td>12  </td> <td>1   </td> <td>3   </td> <td>34  </td> <td>3.8    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>3   </td> <td>Henderson, Taliyah</td> <td>9-0  </td> <td>87  </td> <td>9.7 </td> <td>13-23 </td> <td>0.565</td> <td>4-10   </td> <td>0.4  </td> <td>2-6   </td> <td>0.333</td> <td>5   </td> <td>11  </td> <td>16  </td> <td>1.8    </td> <td>10  </td> <td>0   </td> <td>1   </td> <td>5   </td> <td>0   </td> <td>1   </td> <td>32  </td> <td>3.6    </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>4   </td> <td>Hull, Laila       </td> <td>5-0  </td> <td>43  </td> <td>8.6 </td> <td>4-11  </td> <td>0.364</td> <td>3-6    </td> <td>0.5  </td> <td>1-2   </td> <td>0.5  </td> <td>6   </td> <td>4   </td> <td>10  </td> <td>2      </td> <td>1   </td> <td>0   </td> <td>1   </td> <td>1   </td> <td>2   </td> <td>2   </td> <td>12  </td> <td>2.4    </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (4 rows omitted)</p>"
      ],
      "text/plain": [
       "#    | Player             | GP-GS | MIN  | AVG  | FG-FGA | FG%   | 3FG-FGA | 3FG%  | FT-FTA | FT%   | OFF  | DEF  | TOT  | REB_AVG | PF   | DQ   | A    | TO   | BLK  | STL  | PTS  | PTS_AVG\n",
       "2    | Harris, Nyla       | 9-9   | 233  | 25.9 | 47-81  | 0.58  | 1-4     | 0.25  | 24-30  | 0.8   | 29   | 41   | 70   | 7.8     | 19   | 0    | 11   | 13   | 2    | 17   | 119  | 13.2\n",
       "10   | Kelly, Reniya      | 9-8   | 270  | 30   | 32-88  | 0.364 | 13-33   | 0.394 | 17-19  | 0.895 | 2    | 19   | 21   | 2.3     | 10   | 0    | 18   | 15   | 1    | 12   | 94   | 10.4\n",
       "0    | Grant, Lanie       | 9-8   | 271  | 30.1 | 29-70  | 0.414 | 19-46   | 0.413 | 11-13  | 0.846 | 1    | 18   | 19   | 2.1     | 17   | 0    | 18   | 17   | 0    | 8    | 88   | 9.8\n",
       "21   | Toomey, Ciera      | 9-9   | 235  | 26.1 | 35-72  | 0.486 | 7-21    | 0.333 | 8-13   | 0.615 | 22   | 44   | 66   | 7.3     | 20   | 1    | 13   | 10   | 13   | 3    | 85   | 9.4\n",
       "24   | Nivar, Indya       | 9-9   | 255  | 28.3 | 26-75  | 0.347 | 3-18    | 0.167 | 11-20  | 0.55  | 13   | 27   | 40   | 4.4     | 25   | 1    | 30   | 31   | 3    | 19   | 66   | 7.3\n",
       "17   | Aarnisalo, Elina   | 9-2   | 186  | 20.7 | 24-54  | 0.444 | 5-17    | 0.294 | 7-8    | 0.875 | 2    | 18   | 20   | 2.2     | 11   | 0    | 18   | 14   | 2    | 6    | 60   | 6.7\n",
       "26   | Queiroz, Taissa    | 7-0   | 75   | 10.7 | 12-20  | 0.6   | 0-5     | 0     | 4-4    | 1     | 4    | 12   | 16   | 2.3     | 10   | 0    | 5    | 6    | 1    | 3    | 28   | 4\n",
       "7    | Brooks, Nyla       | 9-0   | 151  | 16.8 | 11-48  | 0.229 | 5-29    | 0.172 | 7-9    | 0.778 | 2    | 18   | 20   | 2.2     | 5    | 0    | 12   | 12   | 1    | 3    | 34   | 3.8\n",
       "3    | Henderson, Taliyah | 9-0   | 87   | 9.7  | 13-23  | 0.565 | 4-10    | 0.4   | 2-6    | 0.333 | 5    | 11   | 16   | 1.8     | 10   | 0    | 1    | 5    | 0    | 1    | 32   | 3.6\n",
       "4    | Hull, Laila        | 5-0   | 43   | 8.6  | 4-11   | 0.364 | 3-6     | 0.5   | 1-2    | 0.5   | 6    | 4    | 10   | 2       | 1    | 0    | 1    | 1    | 2    | 2    | 12   | 2.4\n",
       "... (4 rows omitted)"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "cplayerstats"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "31d8e4ba-5c74-465f-b5f7-ff4463cbb5c8",
   "metadata": {},
   "outputs": [],
   "source": [
    "# correlation between Indya's turnovers to losses... "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "ad58098c-5fb8-4bfb-ad65-d1864cb5220a",
   "metadata": {},
   "outputs": [],
   "source": [
    "gameresults = Table.read_table(\"game_results.csv\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "8f2579c8-dac3-46b4-8746-5dab8cd7ddcd",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Date</th> <th>Opponent</th> <th>Conference</th> <th>W/L</th> <th>Score</th> <th>Attendance</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>11/03/25</td> <td>N.C. CENTRAL       </td> <td>nan       </td> <td>W   </td> <td>90-42</td> <td>6336      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/06/25</td> <td>ELON               </td> <td>nan       </td> <td>W   </td> <td>71-37</td> <td>3111      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/13/25</td> <td>vs UCLA            </td> <td>nan       </td> <td>L   </td> <td>60-78</td> <td>1588      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/15/25</td> <td>vs Fairfield       </td> <td>nan       </td> <td>W   </td> <td>82-68</td> <td>2116      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/20/25</td> <td>at N.C. A&T        </td> <td>nan       </td> <td>W   </td> <td>85-50</td> <td>0         </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/23/25</td> <td>UNC GREENSBORO     </td> <td>nan       </td> <td>W   </td> <td>94-48</td> <td>2418      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/27/25</td> <td>vs South Dakota St.</td> <td>nan       </td> <td>W   </td> <td>83-48</td> <td>0         </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/28/25</td> <td>vs Kansas St.      </td> <td>nan       </td> <td>W   </td> <td>85-73</td> <td>200       </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/29/25</td> <td>vs Columbia        </td> <td>nan       </td> <td>W   </td> <td>80-63</td> <td>0         </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>12/04/25</td> <td>at Texas           </td> <td>nan       </td> <td>L   </td> <td>64-79</td> <td>9020      </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (12 rows omitted)</p>"
      ],
      "text/plain": [
       "Date     | Opponent            | Conference | W/L  | Score | Attendance\n",
       "11/03/25 | N.C. CENTRAL        | nan        | W    | 90-42 | 6336\n",
       "11/06/25 | ELON                | nan        | W    | 71-37 | 3111\n",
       "11/13/25 | vs UCLA             | nan        | L    | 60-78 | 1588\n",
       "11/15/25 | vs Fairfield        | nan        | W    | 82-68 | 2116\n",
       "11/20/25 | at N.C. A&T         | nan        | W    | 85-50 | 0\n",
       "11/23/25 | UNC GREENSBORO      | nan        | W    | 94-48 | 2418\n",
       "11/27/25 | vs South Dakota St. | nan        | W    | 83-48 | 0\n",
       "11/28/25 | vs Kansas St.       | nan        | W    | 85-73 | 200\n",
       "11/29/25 | vs Columbia         | nan        | W    | 80-63 | 0\n",
       "12/04/25 | at Texas            | nan        | L    | 64-79 | 9020\n",
       "... (12 rows omitted)"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "gameresults"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "e2e967ab-e8d8-4ecd-9f7e-83b8dd6c36d1",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Opponent</th> <th>W/L</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>N.C. CENTRAL       </td> <td>W   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>ELON               </td> <td>W   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>vs UCLA            </td> <td>L   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>vs Fairfield       </td> <td>W   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>at N.C. A&T        </td> <td>W   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>UNC GREENSBORO     </td> <td>W   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>vs South Dakota St.</td> <td>W   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>vs Kansas St.      </td> <td>W   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>vs Columbia        </td> <td>W   </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>at Texas           </td> <td>L   </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (12 rows omitted)</p>"
      ],
      "text/plain": [
       "Opponent            | W/L\n",
       "N.C. CENTRAL        | W\n",
       "ELON                | W\n",
       "vs UCLA             | L\n",
       "vs Fairfield        | W\n",
       "at N.C. A&T         | W\n",
       "UNC GREENSBORO      | W\n",
       "vs South Dakota St. | W\n",
       "vs Kansas St.       | W\n",
       "vs Columbia         | W\n",
       "at Texas            | L\n",
       "... (12 rows omitted)"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "gameresults.select('Opponent','W/L')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "195af3a6-93ea-4b7c-849b-70427405411d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Date</th> <th>Opponent</th> <th>W/L</th> <th>Score</th> <th>Attendance</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>11/03/25</td> <td>N.C. CENTRAL       </td> <td>W   </td> <td>90-42</td> <td>6336      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/06/25</td> <td>ELON               </td> <td>W   </td> <td>71-37</td> <td>3111      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/13/25</td> <td>vs UCLA            </td> <td>L   </td> <td>60-78</td> <td>1588      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/15/25</td> <td>vs Fairfield       </td> <td>W   </td> <td>82-68</td> <td>2116      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/20/25</td> <td>at N.C. A&T        </td> <td>W   </td> <td>85-50</td> <td>0         </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/23/25</td> <td>UNC GREENSBORO     </td> <td>W   </td> <td>94-48</td> <td>2418      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/27/25</td> <td>vs South Dakota St.</td> <td>W   </td> <td>83-48</td> <td>0         </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/28/25</td> <td>vs Kansas St.      </td> <td>W   </td> <td>85-73</td> <td>200       </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/29/25</td> <td>vs Columbia        </td> <td>W   </td> <td>80-63</td> <td>0         </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>12/04/25</td> <td>at Texas           </td> <td>L   </td> <td>64-79</td> <td>9020      </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (12 rows omitted)</p>"
      ],
      "text/plain": [
       "Date     | Opponent            | W/L  | Score | Attendance\n",
       "11/03/25 | N.C. CENTRAL        | W    | 90-42 | 6336\n",
       "11/06/25 | ELON                | W    | 71-37 | 3111\n",
       "11/13/25 | vs UCLA             | L    | 60-78 | 1588\n",
       "11/15/25 | vs Fairfield        | W    | 82-68 | 2116\n",
       "11/20/25 | at N.C. A&T         | W    | 85-50 | 0\n",
       "11/23/25 | UNC GREENSBORO      | W    | 94-48 | 2418\n",
       "11/27/25 | vs South Dakota St. | W    | 83-48 | 0\n",
       "11/28/25 | vs Kansas St.       | W    | 85-73 | 200\n",
       "11/29/25 | vs Columbia         | W    | 80-63 | 0\n",
       "12/04/25 | at Texas            | L    | 64-79 | 9020\n",
       "... (12 rows omitted)"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "gameresults.drop('Conference')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "id": "c9992c01-29d7-46ab-903a-949b0175cd5d",
   "metadata": {},
   "outputs": [],
   "source": [
    "indyast= Table.read_table('indya.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "id": "cef703d8-be78-4426-9f3d-ec42a8d99d33",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Date</th> <th>opponet</th> <th>turnovers </th> <th>W/L</th> <th>Home or away</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>11/03/25</td> <td>N.C Centra;     </td> <td>4         </td> <td>W   </td> <td>Home        </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/06/25</td> <td>Elon            </td> <td>3         </td> <td>W   </td> <td>Home        </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/13/25</td> <td>UCLA            </td> <td>1         </td> <td>L   </td> <td>Away        </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/15/25</td> <td>Fairfield       </td> <td>2         </td> <td>W   </td> <td>Away        </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/20/25</td> <td>N.C A&T         </td> <td>4         </td> <td>W   </td> <td>Away        </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/23/25</td> <td>UNC Greensboro  </td> <td>4         </td> <td>W   </td> <td>Home        </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/27/25</td> <td>South Dakota St.</td> <td>1         </td> <td>W   </td> <td>Away-N      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/28/25</td> <td>Kansas St.      </td> <td>1         </td> <td>W   </td> <td>Away-N      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/29/25</td> <td>Columbia        </td> <td>0         </td> <td>W   </td> <td>Away-N      </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>12/04/25</td> <td>Texas           </td> <td>2         </td> <td>L   </td> <td>Away        </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (15 rows omitted)</p>"
      ],
      "text/plain": [
       "Date     | opponet          | turnovers  | W/L  | Home or away\n",
       "11/03/25 | N.C Centra;      | 4          | W    | Home\n",
       "11/06/25 | Elon             | 3          | W    | Home\n",
       "11/13/25 | UCLA             | 1          | L    | Away\n",
       "11/15/25 | Fairfield        | 2          | W    | Away\n",
       "11/20/25 | N.C A&T          | 4          | W    | Away\n",
       "11/23/25 | UNC Greensboro   | 4          | W    | Home\n",
       "11/27/25 | South Dakota St. | 1          | W    | Away-N\n",
       "11/28/25 | Kansas St.       | 1          | W    | Away-N\n",
       "11/29/25 | Columbia         | 0          | W    | Away-N\n",
       "12/04/25 | Texas            | 2          | L    | Away\n",
       "... (15 rows omitted)"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "indyast"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "id": "81ee4da9-b420-4843-9729-18b6cb232a89",
   "metadata": {},
   "outputs": [],
   "source": [
    "def win_to_num(result):\n",
    "    if result == 'W':\n",
    "        return 1\n",
    "    else:\n",
    "        return 0"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "id": "e9021b8d-f1ec-4608-ba68-1f9d659b31df",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table border=\"1\" class=\"dataframe\">\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Date</th> <th>opponet</th> <th>turnovers </th> <th>W/L</th> <th>Home or away</th> <th>WinNum</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>11/03/25</td> <td>N.C Centra;     </td> <td>4         </td> <td>W   </td> <td>Home        </td> <td>1     </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/06/25</td> <td>Elon            </td> <td>3         </td> <td>W   </td> <td>Home        </td> <td>1     </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/13/25</td> <td>UCLA            </td> <td>1         </td> <td>L   </td> <td>Away        </td> <td>0     </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/15/25</td> <td>Fairfield       </td> <td>2         </td> <td>W   </td> <td>Away        </td> <td>1     </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/20/25</td> <td>N.C A&T         </td> <td>4         </td> <td>W   </td> <td>Away        </td> <td>1     </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/23/25</td> <td>UNC Greensboro  </td> <td>4         </td> <td>W   </td> <td>Home        </td> <td>1     </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/27/25</td> <td>South Dakota St.</td> <td>1         </td> <td>W   </td> <td>Away-N      </td> <td>1     </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/28/25</td> <td>Kansas St.      </td> <td>1         </td> <td>W   </td> <td>Away-N      </td> <td>1     </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>11/29/25</td> <td>Columbia        </td> <td>0         </td> <td>W   </td> <td>Away-N      </td> <td>1     </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>12/04/25</td> <td>Texas           </td> <td>2         </td> <td>L   </td> <td>Away        </td> <td>0     </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>\n",
       "<p>... (15 rows omitted)</p>"
      ],
      "text/plain": [
       "Date     | opponet          | turnovers  | W/L  | Home or away | WinNum\n",
       "11/03/25 | N.C Centra;      | 4          | W    | Home         | 1\n",
       "11/06/25 | Elon             | 3          | W    | Home         | 1\n",
       "11/13/25 | UCLA             | 1          | L    | Away         | 0\n",
       "11/15/25 | Fairfield        | 2          | W    | Away         | 1\n",
       "11/20/25 | N.C A&T          | 4          | W    | Away         | 1\n",
       "11/23/25 | UNC Greensboro   | 4          | W    | Home         | 1\n",
       "11/27/25 | South Dakota St. | 1          | W    | Away-N       | 1\n",
       "11/28/25 | Kansas St.       | 1          | W    | Away-N       | 1\n",
       "11/29/25 | Columbia         | 0          | W    | Away-N       | 1\n",
       "12/04/25 | Texas            | 2          | L    | Away         | 0\n",
       "... (15 rows omitted)"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "indyast=indyast.with_column(\n",
    "    'WinNum',\n",
    "    indyast.apply(win_to_num,'W/L')\n",
    ")\n",
    "indyast"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "id": "ead4487f-224e-445a-891d-0742cc2f33f7",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "-0.44273256811044709"
      ]
     },
     "execution_count": 31,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "correlation=np.corrcoef(indyast.column('turnovers '), indyast.column('WinNum'))[0,1]\n",
    "correlation"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "id": "f54560eb-6a05-4b07-aec5-aeb88890ac23",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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GpgULwbPycNw5velaNawRqY1hgb68Jr2k+grKjIcEBERqVG9GlY4tnUh1s4bDbOSwhsJjh/eE1aW5UTvieGAiIhIzXR0dDCwx3e4emgNfuzdHjKZDFaW5TBumJNa+snTLZuJiIgo/5QsYYwVM3/GwB7fITlFrnKVxYLEcEBERKRhvq1XTa3Pz9MKREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCkgkHERER6N27NypVqgQLCws4Ojpi79692f7+S5cuYcaMGWjVqhWsrKxgbm6Opk2bYvbs2YiLiyu4xomIiCRGT90NZMe5c+fg7OwMAwMD9OzZEyYmJjh8+DBcXFzw9OlTTJw4Mct9DBkyBLGxsbC1tUXfvn0hk8lw/vx5rFq1CocOHUJQUBDKlCkjwqshIiLSbBofDuRyOdzc3CCTyXDkyBE0aNAAADBlyhS0b98enp6e6NGjB6ytrVXu55dffkHfvn1Rrly5jG0KhQKTJk2Cr68vlixZAm9v7wJ9LURERFKg8acVQkNDERUVhV69emUEAwAwNjaGu7s75HI5/P39s9zPuHHjBMEAAGQyGdzd3QEAFy5cyN/GiYiIJErjw8H58+cBAI6Ojl89lr4tL2/s+vr6AABdXd1c74OIiEibaPxphcjISADI9LSBqakpzMzMMmpyY8eOHQAyDx+ZSUxMzPVzpUtOThb8l6SHYyh9HEPp4xhmX5EiRXJUr/HhID4+HgBgYmKS6ePGxsaIiYnJ1b5v3ryJJUuWoEyZMhg7dmy2vicmJgapqam5er7/evnyZb7sh9SHYyh9HEPp4xiqpquriypVquToezQ+HBSUx48fo2/fvkhNTYWvry/MzMyy9X0WFhZ5fu7k5GS8fPkS5ubmMDAwyPP+SHwcQ+njGEofx7DgaHw4SD9ikH4E4b8SEhKUHlVQ5unTp+jatSvevHkDPz8/ODg4ZPt7c3poRhUDA4N83R+Jj2MofRxD6eMY5j+Nn5CYPtcgs3kFcXFxiI2NzfIyxn978uQJunTpghcvXmDLli3o0KFDvvVKRESkDTQ+HDRv3hwAEBwc/NVj6dvSa7KSHgyeP3+OzZs3o3PnzvnXKBERkZbQ+HDQqlUrVK5cGfv27cPNmzcztickJGDp0qXQ09ND//79M7bHxsbiwYMHiI2NFezn38HA19cXXbt2Fe01EBERSYnGzznQ09PD6tWr4ezsjE6dOsHZ2RnGxsY4fPgwnjx5Ag8PD1StWjWj3sfHB0uWLMGUKVMwbdq0jO1dunRBdHQ0mjZtitu3b+P27dtfPde/64mIiAorjQ8HAODg4IDjx4/D09MTAQEBSElJQc2aNTFjxgz06dMnW/uIjo4GAFy5cgVXrlzJtIbhgIiICJDFxcUp1N1EYZOYmIjo6GhYWlpyhq1EcQylj2MofRzDgqPxcw6IiIhIXAwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAIMB0RERCTAcEBEREQCDAdEREQkwHBAREREAgwHREREJMBwQERERAKSCQcRERHo3bs3KlWqBAsLCzg6OmLv3r052kdaWhp8fHxgb2+PcuXKwdraGkOHDkVkZGQBdU1ERCQ9kggH586dQ4cOHXDp0iV0794dw4YNQ2xsLFxcXLBs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",
      "text/plain": [
       "<Figure size 500x500 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "indyast.scatter('turnovers ','WinNum', fit_line=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "2449340e-4c5d-4347-8c89-f175d7970859",
   "metadata": {},
   "outputs": [],
   "source": [
    "#with this correlation of -0.44 we can conclude that Indya's turnovers do affect the team's outcome.. low turnover = higher chance of winning. More turnover = lower chance of winning "
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python [conda env:anaconda3] *",
   "language": "python",
   "name": "conda-env-anaconda3-py"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.13.5"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
