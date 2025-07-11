---
title: "Vishwa CTF 2022"
date: 2022-12-28T18:07:47+08:00
draft: false
---

[Home](/)

## The Library - 449 points - OSINT, Cryptography

Description:

Send a ‘hello’ to “The Librarian” from the bot list on the Discord server, and he shall guide you further.

The Library is a 5 level OSINT challenge with hints of ancient/classical cryptography. We are pointed to the discord bot in the Vishwa CTF discord server named “The Librarian”:

### Level 1

After sending a “hello” to the librarian, we get:

> Welcome! Bring me what I ask and I shall take you on a journey across the land of books. Here is the first step - ‘Very few of us are what we seem.’ Tommy is to call on Miss Glen at what time? Give me the time in 12 hr format (HH:MM) (without am/pm) and I will lead you further.

After some searching on ‘Very few of us are what we seem.’, we found that it was from the book “The man in the mist” by Agatha Christie. Looking for the plot of the book from wikipedia, we find that Tommy is to call Miss Glen at 6:10 pm at the White House.

**Answer: 06:10**

It seems that this challenge requires us to research about various books.

### Level 2

> Good job, here is the next part - He appeared to help the Son of Neptune, this seer has a history of helping heroes on their quests. He is also acknowledged in mythology to guide a voyage to retrieve what?

Taking a look at the the Son of Neptune leads us to Rick Riordan’s The Heroes of Olympus series. We found the character Phineas/Phineus. He helped the Argonauts which were trying to find the Golden Fleece on their ship the Argo.

**Answer: golden fleece**

### Level 3

> Well done, here is the next part - ‘The year without a summer, a vacation, and a classic was created.’ In this classic, the names of the creation and creator are often confused. Give me the name of the university where the creator studied and I shall give you the next piece of the puzzle.

The year without a summer is referencing to the volcanic events of 1816 where the volcano Mount Tambora erupted causing ash clouds to cover the skies all over the globe. Searching for “a year without summer classics”, we get [this article](https://www.theguardian.com/music/2016/jun/16/1816-year-without-summer-dark-masterpieces-beethoven-schubert-shelley) that talks about some notable pieces of art and literature made during the time. There was mentions of the book Frankenstein which matched the hint of “creator & creation”. We look up where Victor Frankenstein had his education for the answer.

**Answer: University of Ingolstadt**

### Level 4

> Splendid, here is the next part - What is the name of the dragon?

<center>
<img src="/viking.jpg" alt="vikings">
</center>

Doing some image reverse searching leads us to “Viking Runes”. Decoding the message by hand gives us:

*STAND BY THE GREY STONE WHEN THE THRVSW QNFKQS AND THE SETTIEE SVN HITH THE LAST LIGWT OF DVRINS DAY HILL SWINE VPON THE KEYWOLE*

Looking up this phrase we find the corrected version:

*“Stand by the grey stone when the thrush knocks, and the setting sun with the last light of Durin’s Day will shine upon the key-hole.”*

This quote can be found in The Hobbit/The Lord of the Rings series. The dragon from Lord of the Rings is named Smaug.

**Answer: Smaug**

### Level 5

> Great job on persevering, this is the last part -

<center>
<img src="/masonic.jpg" alt="masonic">
</center>

> These Symbols might make you feel pretty Lost, but not as much as the severed hand right in the

<center>
<img src="/hall.jpg" alt="hall" width="80%" height="80%">
</center>

The 2nd image is an image of Capitol Rotunda. Looking at the capitalized text of the 2nd sentence, it leads us to the book “The Lost Symbol”. Reading the plot of the book, The protagonist finds a severed hand in the middle of Capitol Rotunda, confirming that this is the book we are looking for.

A quick image reverse search finds that the method of cryptography used in the 1st image is the masonic cipher. Decoding it via a website gives us gibberish. After hours of searching, we came across [this video](https://www.youtube.com/watch?v=6fedjvyRt5w&t=2308s&ab_channel=CUNYQueensborough) about the use of the masonic cipher and “magic squares” in The Lost Symbol. The magic squares seem to be used for some sort of transposition cipher. Using Durer’s magic square to position the symbols and then decrypting it via the order of the magic square, we get the final answer.

**Answer: OSINTISPRETTYFUN**

Giving the answer to The Librarian gives us the flag:

> Congratulations on getting through all the challenges, here is your flag. vishwaCTF{b00ks_d0_b3_1nt3r3st1ng!}

