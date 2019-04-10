# UAS Bahasa Pemrograman 1

silakan tuliskan langkah-langkah disertai screenshotnya

# Langkah 1

Ketik link yang tersedia kemudian akan muncul bacaan seperti clone

# ![langkah 1](https://user-images.githubusercontent.com/46734107/55854551-39d19c00-5b8f-11e9-8690-fceaaca6b420.png)

# Langkah 2

Pada tahap ini kita membuat projek baru dengan konfigurasi virtual environment sepeti gambar di bawah ini

# ![langkah 2](https://user-images.githubusercontent.com/46734107/55855084-b31dbe80-5b90-11e9-9daf-aa3fcdb34255.png)

# Langkah 3

Pada tahap ini install pip dari pyCram seperti di bawah ini

# ![langkah 3](https://user-images.githubusercontent.com/46734107/55855257-37704180-5b91-11e9-927a-549954c375b3.png)

# Langkah 4

Pada tahap ini kita membuat kodingan dengan nama main.py dan baseapp.py
 
# kode kodingan main.py
 
 ```
 from core.baseapp import 
 
class App(BaseApp):
    pass

if __name__ == "__main__":
    theApp = App()
    theApp.run()
``` 
 
# Kode kodingan baseapp.py

```
from os import path
import pygame
from core.const import *
from core.enemy import Enemy
from core.player import Player

img_dir = path.join(path.dirname(__file__), '../img')

class BaseApp:
    screen = pygame.display.set_mode((WIDTH, HEIGHT))
    clock = pygame.time.Clock()

    def __init__(self):
        # initialize pygame and create window
        pygame.init()
        pygame.mixer.init()
        pygame.display.set_caption("UAS Bahasa Pemrograman 1")

        # Load all game graphics
        self.background = pygame.image.load(path.join(img_dir, "bg.png")).convert()
        self.background_rect = self.background.get_rect()
        player_img = pygame.image.load(path.join(img_dir, "player.png")).convert()
        meteor_img = pygame.image.load(path.join(img_dir, "meteor.png")).convert()

        BaseApp.all_sprites = pygame.sprite.Group()
        self.enemies = pygame.sprite.Group()
        self.player = Player(player_img)
        BaseApp.all_sprites.add(self.player)
        for i in range(8):
            enemy = Enemy(meteor_img)
            BaseApp.all_sprites.add(enemy)
            self.enemies.add(enemy)

        self.running = False

    def on_playing(self):
        pass

    def stop(self):
        self.running = False

    def check_collision(self, sprite, group, dokill=True):
        return pygame.sprite.spritecollide(sprite, group, dokill)

    def run(self):
        # Game loop
        self.running = True
        while self.running:
            # keep loop running at the right speed
            BaseApp.clock.tick(FPS)
            # Process input (events)
            for event in pygame.event.get():
                # check for closing window
                if event.type == pygame.QUIT:
                    self.running = False

            self.on_playing()

            # Update
            BaseApp.all_sprites.update()

            # Draw / render
            BaseApp.screen.fill(BLACK)
            BaseApp.screen.blit(self.background, self.background_rect)
            BaseApp.all_sprites.draw(BaseApp.screen)
            # *after* drawing everything, flip the display
            pygame.display.flip()

        pygame.quit()
 ```
# Langkah 5

Pada tahap ini kita akan menjalankan eksekusi nya dengan  ketik RUN jika berhasil maka gambarnya di bawah seperti ini:

# ![langkah 5](https://user-images.githubusercontent.com/46734107/55857461-70abb000-5b97-11e9-84cb-11f254170415.png)

