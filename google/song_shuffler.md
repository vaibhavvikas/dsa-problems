## Song Shuffler

Problem Statement:
Given a playlist of songs, you have to design a song shuffler.
This song shuffler is not like the normal song shuffler that shuffles the complete playlist at the start and returns a shuffled list, but instead when asked for a next song to be played, returns a random song from the list of songs.
The next random song to be played should satisfy a condition that the song was not played in the last 'k' turns.
You have to make sure, that at each call, all the eligible (not played during last k turns) songs have equal probability of being played next.

```bash
For example:
if songs = [A, B, C, D], k = 2,
then a possible random sequence of songs can be:

playNext: [ A , B , C , D ] ->  return C
playNext: [ A , B , _ , D ] ->  return A
playNext: [ _ , B , _ , D ] ->  return B
playNext: [ _ , _ , C , D ] ->  return C

(as C was not played in the last two turns, 
it has an equal probability with D to be played).
```
###
```bash
We use the array for the song list.

If anytime we choose a song
we add it into the queue,
adn replace the ind by the last
element of array

Any time if our queue length is gt 
than k we pop and put it at the last
position of the array
```
```
TC: O(1)
SC: O(k)
```

### Solution

```python
import random
from collections import deque

class SongShuffler:

    def __init__(self, songs, k):
        self.songs = songs
        self.k = k
        self.played = deque([])
        self.max_len = len(songs) - 1

    def play_next(self):
        idx = random.randint(0, self.max_len)	
        song_played = self.songs[idx]
        self.songs[idx] = self.songs[self.max_len]
        self.max_len -= 1

        self.played.append(song_played)
        if len(self.played) > self.k:
            self.max_len += 1
            self.songs[self.max_len] = self.played.popleft()

        return song_played
```
