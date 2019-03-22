
class BaseCharacter { //character object constructor
  constructor(name, race, strength, dexterity, charisma, intelligence, type, weapon, power) {
    this.name = name;
    this.race = race;
    this.strength = strength;
    this.dexterity = dexterity;
    this.charisma = charisma;
    this.intelligence = intelligence;
    this.type = type;
    this.weapon = weapon;
    this.power = power;
    this.health = 50;
    this.items = {
      spear: false,
      egg: false,
      sandals: false
    }
  }
  get healthbar() {
    alert(`Healthbar: ${this.health}`);
  }
  set injury(damage) {
    this.health -= damage;
  }
  statShow() {
    let stats = '';
    for (prop in this) {
      if (prop === 'items'){
        continue;
      };
      stats += prop + ': ' + this[prop] + '\n';
    }
    return stats;
  }
}

const charData = { //Object to hold all the character/class stats
  //Race
  'dwarf': ['Dwarf', 3, 1, 1, 4],
  'orc': ['Orc', 4, 2, 0, 1],
  'talking dog': ['Talking Dog', 1, 3, 0, 5],
  'ent': ['Ent', 5, 1, 2, 3],
  //Class
  'warlock': ['Warlock', 'Magic Staff', 'fireballs'],
  'thief': ['Thief', 'Throwing Knives', 'sneak attack'],
  'warrior': ['Warrior', 'Great Sword', 'power swing'],
  'bard': ['Bard', 'Lute Axe', 'heavy metal'],
  //Enemies
  'ogress': 3,
  'bartender': 5,
  'ranger': 8,
  'ranger2': 2,
  'bandits': 12,
  'flood': 14,
  'cave': 8,
  'dragon': 17
}

const charSave = {}; // Empty object to hold the new player info


const gameMechanics = {
  charSelect: function () {
    let name = "";
    let race = "";
    let type = "";
    while (name === "" || race === "" || type === "") {
      alert('Answer these questions three, foolish mortal!');
      name = prompt('What is your character name?');
      race = prompt('Choose your race: Dwarf, Talking Dog, Ent, or Orc');
      type = prompt('Choose your class: Warrior, Bard, Warlock, or Thief');
      if (name === null || race === null || type === null) {
        alert(`Ok, I guess we don't need to play a cool game...`)
        break;
      };
      if (name !== null && charData[race.toLowerCase()] && charData[type.toLowerCase()]) {
        charSave.newPlayer = new BaseCharacter(name, ...charData[race.toLowerCase()], ...charData[type.toLowerCase()]);
        if (charSave.newPlayer.type === 'Bard') {
          charSave.newPlayer.charisma += 2;
        } else if (charSave.newPlayer.type === 'Warrior') {
          charSave.newPlayer.strength += 2;
        } else if (charSave.newPlayer.type === 'Thief') {
          charSave.newPlayer.dexterity += 2;
        } else if (charSave.newPlayer.type === 'Warlock') {
          charSave.newPlayer.intelligence += 2;
        };
        alert(`Nice to meet you ${name} the ${race} ${type}!`);
        alert(charSave.newPlayer.statShow());
        break;
      }
    }
  },
  dieRoll: () => {
    roll = Math.floor((Math.random() * 20) + 1);
    return roll;
  },
  skillCheck: function (chapter, scene, responseLow, enemy) {
    const encounter = plotLine[chapter][scene][responseLow]['encounterType'];
    const rand = this.dieRoll();
    alert(`You rolled a ${rand} on your ${encounter} check!`)
    const skillPoint = charSave.newPlayer[encounter];
    if (rand + skillPoint >= charData[enemy]) {
      return true;
    } else {
      return false;
    }
  },
  choice: ask => prompt(ask),
  storyScene: function (chapter, scene, enemy, item) {
    alert(plotLine[chapter][scene]['opener']);
    //story opener
    let response = "";
    //repeat until string response
    while (response === "" || !plotLine[chapter][scene][response]) {
      //prompt scene question to user
      response = this.choice(plotLine[chapter][scene]['question']);
      if (response === null) {
        break;
      };
      if (response !== null && response !== "") {
        //if string response, set to lowercase
        let responseLow = response.toLowerCase();
        if(response !== null && response !== "" && plotLine[chapter][scene]['riddle']){
          this.storyRiddle(chapter, scene, responseLow, item);
          if (plotLine[chapter][scene]['closer'] && charSave.newPlayer.health > 0 && charSave.newPlayer.health <= 50) {
            alert(plotLine[chapter][scene]['closer']);
          };
          break;
        } else if (response !== null && response !== "" && plotLine[chapter][scene][response.toLowerCase()]) {
          this.storyChoice(chapter, scene, responseLow, enemy, item);
          if (plotLine[chapter][scene]['closer'] && charSave.newPlayer.health > 0 && charSave.newPlayer.health <= 50) {
            alert(plotLine[chapter][scene]['closer']);
          };
          break;
        };
      };
    };
    return;
  },
  storyChoice: function (chapter, scene, responseLow, enemy, item) {
    const success = this.skillCheck(chapter, scene, responseLow, enemy);
    //successful outcome
    if (success === true) {
      alert(plotLine[chapter][scene][responseLow]['success']);
      if (plotLine[chapter][scene][responseLow]['item'] = item){
        charSave.newPlayer.items[item] = true;
        console.log(charSave.newPlayer.items[item]);
      };
    } else if (plotLine[chapter][scene]['itemSave']) {
      const checkItem = plotLine[chapter][scene][responseLow]['itemSave']['item'];
      console.log(checkItem);
      if (charSave.newPlayer.items[checkItem]){
        alert(plotLine[chapter][scene]['itemSave'][pass]);
      } else {
        alert(plotLine[chapter][scene][responseLow]['fail']);
        charSave.newPlayer.injury = plotLine[chapter][scene][responseLow]['injury'];
        charSave.newPlayer.healthbar;
      };
    } else {
      alert(plotLine[chapter][scene][responseLow]['fail']);
      charSave.newPlayer.injury = plotLine[chapter][scene][responseLow]['injury'];
      charSave.newPlayer.healthbar;
    };
    return;
  },
  storyChoice: function (chapter, scene, responseLow, enemy, item) {
    const success = this.skillCheck(chapter, scene, responseLow, enemy);
    //successful outcome
    if (success === false && plotLine[chapter][scene]['itemSave']) {
      const checkItem = plotLine[chapter][scene][responseLow]['itemSave']['item'];
      console.log(checkItem);
      if (charSave.newPlayer.items[checkItem]){
        alert(plotLine[chapter][scene]['itemSave'][pass]);
      } else {
        alert(plotLine[chapter][scene][responseLow]['fail']);
        charSave.newPlayer.injury = plotLine[chapter][scene][responseLow]['injury'];
        charSave.newPlayer.healthbar;
      };
    } else if (success === true) {
      alert(plotLine[chapter][scene][responseLow]['success']);
      if (plotLine[chapter][scene][responseLow]['item'] = item){
        charSave.newPlayer.items[item] = true;
      };
    } else {
      alert(plotLine[chapter][scene][responseLow]['fail']);
      charSave.newPlayer.injury = plotLine[chapter][scene][responseLow]['injury'];
      charSave.newPlayer.healthbar;
    };
    return;
  },
  storyRiddle: function (chapter, scene, responseLow, item) {
    const success = (responseLow === plotLine[chapter][scene]['riddle']['answer']);
    if (success === true) {
      alert(plotLine[chapter][scene]['riddle']['success']);
      charSave.newPlayer.items[item] = true;
      } else {
      alert(plotLine[chapter][scene]['riddle']['fail']);
    };
    return;
  }
}

gameMechanics.charSelect();

//Object to hold all of our responses and story alerts
const plotLine = {
  storyOpener: `You drunkenly awake moments before dawn. Your face is sunken into the sharp pebble road. You think about your life choices. Your inheritance you received yesterday and all the mead you drank las-\n...Your inheritance \nYour 500 gold pieces are gone... \nAt least you still have your trusty ${charSave.newPlayer.weapon}.`,
  tavernChapter: {
    tavernScene1: {
      opener: `You step inside the dim pub. \nDifferent fantastical creatures are hunched over, slurping on their ales, and sinking into their day drinking habits.`,
      question: `Do you want to:\nA: Smooth talk the ogress nearby.\nB: Smooth talk her unattended, half-empty stein of mead.`,
      a: {
        encounterType: 'charisma',
        success: `You smith up a romantic verse. “When the monks said your body is a temple, they weren’t kidding!” The Ogress, hands you her address on a parchment paper. `,
        fail: `You fumble with your words. \n \“Damn, girl, you large... uh, In a good way, for your kind, I mean...\” \n The Ogress throws her grog in your face. You’re now soaked in more than shame.`,
        injury: 2,
      },
      b: {
        encounterType: 'charisma',
        success: `You taste the familiar flavor of ogre backwash. Mmmmm, mucusy.`,
        fail: `It's a trap! She poisoned the mead with iocane powder! Luckily, you've been developing an immunity over the last few years and you only get a slight headache.`,
        injury: 2
      }
    },
    tavernScene2: {
      opener: `You step up to the bar and the bartender collapses in height.\nYou look over the bar only to discover he is an old hobbit leaning against a stack of step ladders.`,
      question: `Bartender: Well, if it isn’t the big spender from last night!\n What happened? Did ye found out buying rounds for the entire pub isn't sustainable?\nYou say:\nA: Your height isn't sustainable!\nB: Actually, I was robbed of all my gold last night. Could you help me?`,
      a: {
        encounterType: 'charisma',
        success: `Bartender: I outta wallop you for that, but it just so happens a fool like you might be useful.`,
        fail: `The bartender jumped over the bar like a 4'2 ninja and shanked you. You bled out on the floor while the town doctor sipped on a pint in the corner.`,
        injury: 50
      },
      b: {
        encounterType: 'charisma',
        success: `Bartender: We’ve all been there, friend. Happens every weekend, now that I think about it... \nLook, since you gave me a good amount before losing it, I’ll help.`,
        fail: `The bartender boxes your right ear before you know what's happening.\n Bartender: I'll help you learn some common sense, kid!`,
        injury: 5
      }
    },
    tavernScene3: {
      opener: `Bartender: Listen here, ${charSave.newPlayer.name}. There’s a Ranger in yon corner, offering a big reward for some quest that's got the Mayor all worked up.\nTold me to send him the best people. I’ll put in a good word for ye if you give me a cut.`,
      question: `You walk up towards the Ranger, he seems unfazed. In a flash, he grabs and chucks his mug at your face!\nDo you want to:\nA: Duck!\nB: Use your ${charSave.newPlayer.weapon} to hit that mug back to his smug face.`,
      a: {
        encounterType: 'dexterity',
        success: `You dodge the mug like a legendary hero from bards’ songs. Angrily, you approach the Ranger.`,
        fail: `The mug smashes on your head and blood streams down your face. You do your best to maintain a tough facade in front of the tavern on-lookers. "Tis' only a flesh wound!", you announce to the disinterested crowd.`,
        injury: 10
      },
      b: {
        encounterType: 'strength',
        success: `Your mighty swing connects right to the mug and it explodes into hundreds of shards. The Ranger's face is strew with glass and blood, yet he looks at you with a crazed grin.`,
        fail: `You take a mighty swing and a miss! The mug smashes on the wall next to your head and showers in glass and ale. Embarassing. You scrape together what's left of your dignity and storm over to the Ranger, weapon in hand.`,
        injury: 10
      }
    },
    tavernScene4: {
      opener: `Ranger: Ha! You're funny. Look, the Mayor of this town lost his Sparkly Golden Thong and needs it back. Word has it, they're in a cave up at the top of the Smoky Mountain...I didn't even want to know why.\nI'm not in this life for the of fetching thongs, gold or no. You can get all the rewards, just say I did it.`,
      question: `You say:\nA: I hate you.\nB: I'll do it! For the money, of course.\nC: All of this seems tiresome.`,
      a: {
        encounterType: 'intelligence',
        success: `Ranger: Great! On you go! Through those woods, then past the valley and up the mountain. Child's play for an adventurer like you! Ta-ta!`,
        fail: `The ranger chops your head clean off! Try to sass him now, smart stuff. `,
        injury: 50
      },
      b: {
        encounterType: 'intelligence',
        success: `Ranger: Great! On you go! Through those woods, then past the valley and up the mountain. Child's play for an adventurer like you! Ta-ta!`,
        fail: `Ranger: MONEY?! Being an adventurer is about GLORY and HONOR. BEGONE WITH YE, SCUM.`,
        injury: -50
      },
      c: {
        encounterType: 'intelligence',
        success: `Ranger: Great! On you go! Through those woods, then past the valley and up the mountain. Child's play for an adventurer like you! Ta-ta!`,
        fail: `Ranger: Great! On you go! Through those woods, then past the valley and up the mountain. Child's play for an adventurer like you! Ta-ta!`,
        injury: 0
      },
      closer: `He leads you to the back door where a dark, thick forest stretches out into the distance. What have you gotten yourself into?`,
    }
  },
  banditChapter: {
    banditScene1: {
      opener: `While trekking through the forest on the main road, you start to get the feeling you are being watched. You hear a "WHOOSH" as an arrow comes flying out of the bushes going right past your ear and into a nearby tree. A group of bandits pop out of the trees and bushes alongside the road and you're quickly surrounded!`,
      question: `Would you like to \nA: Fight them with your bare hands!\nB: Beg for forgiveness\nC: Scream and sprint for your life!\nD: Quickly draw out your ${charSave.newPlayer.weapon} and use the power of ${charSave.newPlayer.power}.`,
      a: {
        encounterType: 'strength',
        success: `You storm through them with your trusty weapon and slaughter them like animals. Gruesome. As you loot their bodies for loose change, you notice a spear on the ground that looks familiar...can it be??\nYou saw a reward poster in town for the stolen Spear of Grognar, the ancient weapon of the legendary orc hero. It must be the same! You bundle it on your back and continue your journey.`,
        fail: `The bandits overwhelm you with numbers; killing you and eating your remains back at their campsite. Don't mess with cannibals in the woods.`,
        injury: 50,
        item: 'spear'
      },
      b: {
        encounterType: 'charisma',
        success: `You slowly talk your way out of hotwater with the bandits by telling them your favorite limericks. Eventually they invite you back to their camp for mead and merrymaking. After you make the bandits Eggs ala ${charSave.newPlayer.name} in the morning, you continue on your journey.`,
        fail: `The bandits can sense your bullshit and are very pissed off, resulting in one of them shooting an arrows at you as you serpentine into the distance. They hit you with an arrow to the knee! DAMN.\nYou bandage your wound and continue on your journey.`,
        injury: 20
      },
      c: {
        encounterType: 'intelligence',
        success: `"Jet fuel can't melt steel beams!", you scream. The bandits stare at each other confused, not noticing that you've already fled the scene.`,
        fail: `You scream, "I LOVE LAMP!" And the bandit leader decides you must be some kind of simpleton and you clearly have no money anyway. They beat you up for they fun of it and disappear back into the woods.\n Bruised in more places than just your pride, you limp your way down the path.`,
        injury: 20
      },
      d: {
        encounterType: 'dexterity',
        success: `You quickly grab your ${charSave.newPlayer.weapon}, and use the full force of ${charSave.newPlayer.power} power on the nearest bandit. He instantly drops dead and the rest of the bandits run off terrified. You're a legend, ${charSave.newPlayer.name}!\nYou loot the body for loose change and continue on your way.`,
        fail: `You attempt to attack them in an unhinged frenzy, but fail miserably. You are easliy defeated as the bandits turn you into a human pin cushion.`,
        injury: 50
      }
    }
  },
  croneChapter: {
    croneScene1: {
      opener: `As you finally emerge from the forest, you spot an old crone sitting by the side of the road. Surprised to see anyone this far out in the countryside, you decide to greet her and ask her if she needs any help...`,
      question: `Crone: How kind of you to ask! Thoughtful adventurers are so rare these days...most can only think of treasure. I need nothing, but I sense that you are seeking something special. I may be able to help if you can answer me this riddle with one word.\nThe more you take, the more you leave behind. What am I?`,
      riddle: {
        answer: 'footsteps',
        success: `Crone: Yes! You are a clever one, aren't you. Take this as your prize and keep it warm.\nShe reaches under her cloak and hands you a Golden Dragon Egg. You can feel something moving inside as you wrap it in a cloth and store it in your sack. As you look up to thank her, the crone has disappeared. Before anything else weird can happen you hightail it down the road!`,
        fail: `Crone: No, I'm sorry dear, that's not the answer! Too bad...too bad. Here, have a banana instead. Potassium is good for you.\nAs you look up to thank her, the crone has disappeared. Before anything else weird can happen you hightail it down the road!`,
        item: 'egg'
      }
    }
  },
  floodChapter: {
    floodScene1: {
      opener: `You feel a splash of cold water hit your nose and lightning cracks the sky. The clouds darken, drenching the land in heavy rainfall. You look at your surroundings and realize that you are in a wash with the water quickly rising around your ankles! You spot the opposite bank, a steep wall of boulders leading to higher ground. Will you climb them to safety before the flood sweeps you away??`,
      question: `Would you like to:\nA: Climb like your life depends on it? (Spoiler: It does.)\nB: Try to outrun the flood and look downstream for an easier crossing?\nC: Wait this one out. Flood shmud, you've seen bigger.`,
      a: {
        encounterType: 'strength',
        success: `No time like the present! Slowly you make your way up the wall, carefully choosing one hold after the other. It's so slippery you might as well have eels for hands. Eel Hands the ${charSave.newPlayer.race} they would call you...\nAnyway, you feel your hand reach over the edge of the wall, find a knarled bush to grab onto, and hoist yourself over the edge. After a quick victory dance, you head off up the mountainside towards fate.`,
        fail: `No time like the present! Slowly you make your way up the wall, carefully choosing one hold after the other. It's so slippery you might as well have eels for hands. Eel Hands the ${charSave.newPlayer.race} they would call you...\nThe wall is becoming more and more treacherous. First your right foot slips, then your weight lurches to the side as you lose your grip. Hurtling through the air toward the ground you think to yourself, "EEL FEEEEEET"`,
        injury: 50
      },
      b: {
        encounterType: 'dexterity',
        success: `You spot a tree downstream with a branch that extends over the top of the boulder wall. You scamper up the tree, across the branch, and drop down to safety at the top of the wall. The flash flood comes rushing through the wash and drowning everything in it's path. You would have been toast! Yikes!\nAs you turn around a pair of ornate Winged Sandals magically appear before you. Your daring escape must have earned the favor of the gods! You thank the Goddess of Luck, don the sandals, and head up the mountain.`,
        fail: `You decide to head downstream a little to see if you can find an easier climb, but you are caught by a sudden flash flood rushing towards you. You run to a nearby tree and get as high as you can while holding on for dear life!\nYou hear a thunderous craking sound as you and the tree come crashing down, yet you keep your grip. The fallen tree has now formed a bridge to the other side! Banged up and scared out of your wits you cross the tree and continue on up the mountain to a questionable future.`,
        injury: 15,
        item: 'sandals'
      },
      c: {
        encounterType: 'charisma',
        success: `The water begins to rise in earnest and here you are looking like a dope without a plan! Luckily, the gods have smiled upon your brazen apathy. Just as a flash flood comes careening towards you, a huge gust of wind lifts you up and safely deposits you at the top of the boulder pile. You quickly say a prayer of thanks the Goddess of Luck, and head up the mountain.`,
        fail: `The wash is filling up fast, but you decide to use that to your advantage and wait for the water to rise high enough to carry you out of the wash. Suddenly, a flash flood comes careening towards you and you are struck from behind by a big rock. You are swept off your feet and hurtle downstream with the current. As you start to lose consciousness, you realize that you might have made the wrong choice.`,
        injury: 50
      }
    }
  },
  dragonChapter: {
    dragonScene1: {
      opener: `The day wears on as you begin to ascend the mountain. Higher and higher you climb, while seeing puffs of smoke coming from the distant top. When you finally reach the last crest you see a cave...`,
      question: `Do you want to:\n A.Go inside the cave.\nB. Go back home and rethink your life choices.\nC. Jump off the cliff.`,
      a: {
        encounterType: 'dexterity',
        success: `You slowly creep inside the cave with your ${charSave.newPlayer.weapon} in one hand and a makeshift torch in the other. You begin to see piles of gold scattered around. The golden treasures are more wondurous the deep you go, but the heat of the place is also rising...`,
        fail: `You get out your ${charSave.newPlayer.weapon} and slowly creep inside the cave. You stumble through the darkness getting a few scrapes along the way. You begin to see piles of gold scattered around.The golden treasures are more wondurous the deep you go, but the heat of the place is also rising...`,
        injury: 2
      },
      b: {
        encounterType: 'intelligence',
        success: `Just as you are about to head down the mounain, you remember a piece of wisdom you once heard: "Three great forces rule the world: stupidity, fear, and greed." You have a change of heart and you decide to let greed win this round. With a makeshift torch in hand, you head into the cave.\nYou begin to see piles of gold scattered around. The golden treasures are more wondurous the deep you go, but the heat of the place is also rising...`,
        fail: `You go back down the mountainside, go home to your little cabin, and ne'er darken the door of an ethically suspect establishment or a dragon's cave again.\n You got your safe ending. HAPPY  NOW??`,
        injury: -50
      },
      c: {
        encounterType: 'charisma',
        success: `Just as you are about to throw yourself of the edge, a large gust of wind pushes you off your feet and onto your backside. Surely this is a sign from the gods! You must push forward with in your quest.\nWith a makeshift torch in hand, you head into the cave. You begin to see piles of gold scattered around. The golden treasures are more wondurous the deep you go, but the heat of the place is also rising...`,
        fail: `You swan dive into the rocks below. What was your plan exactly? Gods, you're terrible at this.`,
        injury: 50
      }
    },
    dragonScene2: {
      opener: `You turn a corner and see the mighty Dragon sleeping on top of it's horde of stolen golden goods including...the Mayor's SPARKLY GOLDEN THONG.`,
      question: `This is it ${charSave.newPlayer.name}, the moment you've been fighting your way to! But the dragon actually looks kind of cute while it's not terrorizing the countryside. Do you:\nA: Try to sneak past it and grab the Mayor's fancy panties\nB: Talk to the dragon and see if you can reason with it.\nC: Attack the damn monster and get this over with.`,
      a: {
        encounterType: 'dexterity',
        success: `You're so slick you slip right past the dragon without it ever waking up! \n Silently you write on the wall with a piece of charcol: Dragonz R DUMB \n ${charSave.newPlayer.name} RULEZ \n You tip toe back out of the cave completely unnoticed.`,
        itemSave: {
          pass: `As you try to slide the thong from under the dragon's paw, you slip on some gold coins! As the sleeping dragon suddenly becomes an awake and very angry dragon, your feet shoes begin to stir. The Winged Sandals! They begin to flap their little wings at a hummingbird's pace and you are lifted off the ground. You snatch those fancy panties from the shocked dragon and soar out of the cave before it can make a move. The Goddess of Luck must really have a thing for you!`,
          item: 'sandals'
        },
        fail: `As you try to slide the thong from under the dragon's paw, you slip on some gold coins! What a klutz. You totally blew it and the dragon wakes up. The dragon roasts you like a marshmellow. `,
        injury: 50
      },
      b: {
        encounterType: 'intelligence',
        success: `You lightly clear your throat and the dragon wakes up. You introduce yourself and begin to explain to the dragon about your quest and what a terrible day you've had. You find the dragon to be a surprisingly empathetic ear.\nYou and the dragon talk for hours since it turns out the two of you really have a lot in common. At the end of a romantic evening together, you decide that what you wanted all along wasn't gold. It was a loving partner...like this dragon.\nYou forget all about the quest and the two of you decide to get hitched. Good luck you crazy lovebirds!`,
        itemSave: {
          pass: `You call out to the dragon and ask for a moment of it's time. As the sleeping dragon suddenly becomes an awake and very angry dragon, you realize trying to talk to a dragon is a life-endingly terrible idea.\nYou quickly pull out the Golden Dragon Egg from your sack and offer the dragon a trade; the egg for the underoos. The dragon, overcome with joy at the idea of parenthood and "too full to eat you anyway", decides to take the trade. Grab the Mayor's delicates and make a run for the exit, dummy!`,
          item: 'egg'
        },
        fail: `You call out to the dragon and ask for a moment of it's time. As the sleeping dragon suddenly becomes an awake and very angry dragon, you realize trying to talk to a dragon is a life-endingly terrible idea.\nYou panic and pretend to be going from cave to cave selling flood insurance. The dragon demands that the pathetic creature before it depart before it decides to roast you. You leave the cave empty handed and spend the rest of your life thinking of better things you could have said in that moment.`,
        injury: -50
      },
      c: {
        encounterType: 'strength',
        success: `HOLY TOLEDO! You go full on berserker on that dragon and hit it from all directions. Before the poor dope even gets its mouth open, you use your ${charSave.newPlayer.power} skills to smash it right in the freaking face with your ${charSave.newPlayer.weapon}. The dragon starts to cry that it doesn't want any trouble and it's ready to give you whatever you want. You grab those golden underoos and strut right out of the cave. GANGSTER.`,
        itemSave: {
          pass: `As you charge the dragon with your ${charSave.newPlayer.weapon}, you slip on some gold coins! The sleeping dragon suddenly becomes an awake and very angry dragon, you realize trying to charge a freaking dragon with no plan is a life-endingly terrible idea.\nBut wait! You remember your Spear of Grognar and throw it directly through the dragon's exposed throat. Amazing shot! Truly, you are the next Grognar. The dragon retreats in pain deep into the cave as you snatch the golden underoos and run outta there.`,
          item: 'spear'
        },
        fail: `As you charge the dragon with your ${charSave.newPlayer.weapon}, you slip on some gold coins! The sleeping dragon suddenly becomes an awake and very angry dragon, you realize trying to charge a freaking dragon with no plan is a life-endingly terrible idea. You totally blew it and the dragon roasts you like a marshmellow.`,
        injury: 50
      }
    }
  },
  storyEnding: {
    partA: `You make it back to town without running into any more trouble. You stride into the Mayor's house knowing that you will finally be richly rewarded for your many trials.\n \n The Mayor is overjoyed if somewhat embarrassed to see you and quickly stashes the treasured Sparkly Golden Thong in the dresser. he leads you out to the center of town...`,
    partB: `And you are presented with a key to the city and all the riches this modest little town has to offer! The Mayor hands you a key and a SACK OF POTATOES. You try no to look to disappointed as look around and realize this town is actually dirt poor. In fact it was likely the townspeople that robbed you to begin with. \n \n You decided you've really had enough adventure for one day and head into the tavern to see how many ales you can buy with a sack of potatoes.`
  }
}

const scenes = [['tavernChapter', 'tavernScene1', 'ogress'], ['tavernChapter', 'tavernScene2', 'bartender'], ['tavernChapter', 'tavernScene3', 'ranger'], ['tavernChapter', 'tavernScene4', 'ranger2'], ['banditChapter', 'banditScene1', 'bandits', 'spear'], ['croneChapter', 'croneScene1', 'none', 'egg'], ['floodChapter', 'floodScene1', 'flood', 'sandals'], ['dragonChapter', 'dragonScene1', 'cave'], ['dragonChapter', 'dragonScene2', 'dragon']];

function gameRun() {
  alert(plotLine.storyOpener);
  for (const scene of scenes) {
    if (charSave.newPlayer.health <= 0 || charSave.newPlayer.health > 50); {
      if (charSave.newPlayer.health <= 0) {
        alert(`You're dead! Enjoy the afterlife`);
        break;
      } else if (charSave.newPlayer.health > 50) {
        alert(`You survived! \n Game Over`);
        break;
      };
    };
    gameMechanics.storyScene(...scene);
    if (scenes.indexOf(scene) === scenes.length - 1) {
      alert(plotLine.storyEnding.partA);
      alert(plotLine.storyEnding.partB);
      alert(`You survived! \n Game Over`);
    }
  };
  replay();
};

function replay() {
  replay = prompt('Would you like to play again? \n Yes or No');
  if (replay === null || replay === "" || replay.toLowerCase() !== 'yes') {
    alert(`Fairwell, adventurer!`);
    return;
  } else if (replay.toLowerCase() === 'yes') {
    gameMechanics.charSelect();
    gameRun()
    ;
  }
};

 function gameMaster() {
  if (charSave.newPlayer) {
    gameRun();
  } else {
    return;
  };
};

gameMaster()
