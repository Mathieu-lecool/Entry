# Entry
An Entry for your Pygame Projects.
This entry adapts to the text that is entered.

# How to use
Declare the variable and enter the **Surface** and the **Rectangle** of the entry.
`entry = Entry(screen, pygame.Rect(25, 85, 150, 30))`

For create and update, use `entry.update()`

For writing text, use **entry()** and insert **event** ( pygame.event.get() )
`entry.entry(event)`

For return the text, use `entry.get()`

For configure the entry, use **config()** and insert optional args (color, border_radius, margin).
`entry.config((0,0,255), 10, 7)`

# Exemple

`
screen = pygame.display.set_mode((200, 200))
entry = Entry(screen, pygame.Rect(25, 85, 150, 30))

entry.config((0,0,255), 10, 7)

while True:

    entry.update()
    pygame.display.flip()

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
          pygame.quit()
        elif event.type == pygame.KEYDOWN:
          entry.entry(event)`
