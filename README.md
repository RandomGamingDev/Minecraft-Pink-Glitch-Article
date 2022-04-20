# Minecraft-Pink-Glitch-Article
An article on github about Minecraft Bedrock's pink glitch. Why is it on github? IDK. I just put it here.

  The reason I made this article is because I haven't seen many things online that explain what exactly is going on, or what they think is going on, so this article will provide a deep dive into the infamous pink glitch. After doing some simple tests I found that by unloading and reloading chunks with those custom 3d models, whether by repeatedly walking away and to them, using an NPC to teleport, spamming /hub, or anything else would eventually cause the pink glitch after enough attempts (There are other ways to trigger it without loading and unloading chunks). What was interesting was that the game became laggier and laggier as I did this. After checking the resources that the game was consuming I realized that the amount of memory used would go up by a substantial amount each time a chunk with these custom 3d models was reloaded, and that this memory wasn't getting freed even after unloading the chunks. I also found that pink glitch would occur when your computer got to around 100% memory usage. From these experiments what I think is causing this glitch is a memory leak.
  Basically, in C++ you have to manually manage memory on the heap, which means that you will get a memory leak if you don't deallocate it, which will cause the memory usage to increase, eventually causing bugs, errors, and then a crash. Here's a simplified example of how something like that would work in C++:
```
#include<iostream>

int main(){
  while (true){
    new Data(); //Represents you loading the chunk (Note: "Data()" is just a placeholder in this example)
    std::cin.get(); //Represents you unloading the chunk
  }
}
```
In this example you got some data that gets loaded onto the heap, and then you can press enter to load more data, the problem is that that old data doesn't get freed from the heap, thus just piling up, causing a memory leak, which as mentioned before is bad.
