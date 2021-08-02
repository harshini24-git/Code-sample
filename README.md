# Code-sample
mport random

# A card has a suit ("Hearts", "Diamonds", "Spades", "Clubs") and a value between 1 and 14
class Card:
  def __init__(self,suit,val):
    self.suit = suit
    self.value = val
    assert val<=13 and val>=1, "invalid card value"
    assert suit in ["Hearts", "Diamonds", "Spades", "Clubs"], "invalid card suit"
  def show(self):
    ''' Show the Current Card '''
    print(str(self.value)+" of "+self.suit)


class Deck:
  def __init__(self):
    ''' Initialize a deck of 52 cards '''
    self.cards = []
    self.build()
  def build(self):
    self.cards = []
    suits = ["Hearts", "Diamonds", "Spades", "Clubs"]
    for s in suits:
      for v in range(1,14):
        self.cards.append(Card(s,v))
  def shuffle(self):
    ''' Shuffle the cards in the deck '''
    for i in range(len(self.cards)):
      ind = random.randint(0,len(self.cards)-1)
      temp = self.cards[i]
      self.cards[i] = self.cards[ind] 
      self.cards[ind] = temp
  def show(self):
    ''' Print the current cards in the deck '''
    for card in self.cards:
      card.show()  
  def drawCard(self):
    ''' Draw the topmost card from the deck '''
    assert len(self.cards)!=0, "Empty Deck!"
    return self.cards.pop()
  def deal(self,players,cards_per_player):
    ''' Distribute cards among the players 
        players = a list fo Players
        cards_per_player = number of cards each player gets'''
    assert cards_per_player*len(players)<=52, "invalid number of cards per player"
    for i in range(cards_per_player):
      for player in players:
        player.draw(self)


class Player:
  def __init__(self,name):
    ''' Initialize a player with the given name '''
    self.name = name
    self.hand = []
  def draw(self,deck):
    ''' Draw a card from the given deck, it will be added in player's hand'''
    self.hand.append(deck.drawCard())
  def showHand(self):
    ''' Show the current cards in Player's hand '''
    for card in self.hand:
      card.show()



if __name__ == "__main__":
  deck = Deck()
  p1 = Player("X")
  p2 = Player("Y")
  p3 = Player("Z")
  
  deck.shuffle()
  deck.deal([p1,p2,p3],3)
  print(p1.name)
  p1.showHand()
  print(p2.name)

  p2.showHand()
  print(p3.name)

  p3.showHand()
