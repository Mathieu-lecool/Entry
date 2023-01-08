# Entry
An Entry for your Pygame Projects.
This entry adapts to the text that is entered.

# How to use
Declare the variable and enter the **Surface** and the **Rectangle** of the entry.
```
entry = Entry(screen, pygame.Rect(25, 85, 150, 30))
```

For create and update, use `entry.update()`

For writing text, use **entry()** and insert **event** ( pygame.event.get() )
```
entry.entry(event)
```

For return the text, use `entry.get()`

For configure the entry, use **config()** and insert optional args (color, border_radius, margin).
```
entry.config((0,0,255), 10, 7)
```

# Exemple

```
import pygame

class Entry:

    pygame.init()

    def __init__(self, surface, rect):
        self.screen = surface
        self.rect = rect
        self.texte = ["", ""]
        self.config()

    def config(self, color=(255,255,255), border_radius=5, margin=4): self.color, self.border_radius, self.margin = color, border_radius, margin
    def get(self): return self.texte[0]

    def entry(self, event):
        if event.key == pygame.K_BACKSPACE: self.texte[0] = self.texte[0][:-1]
        else: self.texte[0] += event.unicode

    def update(self):
        pygame.draw.rect(self.screen, self.color, self.rect, border_radius=self.border_radius)
        self.texte[1] = self.texte[0]
        txt = pygame.font.Font(None, self.rect.height-6)
        while txt.size(self.texte[1])[0] > self.rect.width-self.margin*2:
            temp, nb = "", 1
            for lettre in self.texte[1]:
                if nb == 1: pass
                else: temp += lettre
                nb += 1
            self.texte[1] = temp
        self.screen.blit(txt.render(self.texte[1], True, (0,0,0)), (self.rect.x+self.margin, self.rect.y+self.rect.height/2-int(txt.size(self.texte[1])[1]/2)))


screen = pygame.display.set_mode((200, 200))
entry = Entry(screen, pygame.Rect(25, 85, 150, 30))

while True:
    entry.update()
    pygame.display.flip()

    for event in pygame.event.get():
        if event.type == pygame.QUIT: pygame.quit()
        elif event.type == pygame.KEYDOWN: entry.entry(event)
```
