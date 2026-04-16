---
layout: default
title: Worldbuilding / Adventuring
nav_order: 8
---

# Worldbuilding And Adventuring
{: .no_toc }

*See first with your mind, then with your eyes, and finally with your body.*
\- Yagyu Munenori

1. TOC
{:toc}

The following pages include tools, tables, and advice for Guides running Ikezu-Ishi. This chapter offers resources and instructions for creating adventures and building dynamic worlds.

## Scenario Start Generator

{: .note }
Inspired by: Sean Wills, “Random Ruins & Ronin Scenario Starts Generator,” Swords and Wizardry, archived March 31, 2016.

The Guide may use the following table to create the beginning of a scenario, providing a starting location, a contact, and a mission.

### The players meet in a village \[LOCATION\] with \[CONTACT\] who speaks of \[EVENT\] caused by \[CAUSE\].

| D10    | LOCATION  | D10 | CONTACT           | D10 | EVENT         | D10 | CAUSE         |
|:-------|:----------|:----|:------------------|:----|:--------------|:----|:--------------|
| **1**  | Market    | 1   | Village Elder     | 1   | Plague        | 1-2 | Monsters      |
| **2**  | Tea House | 2   | Monk              | 2   | Rebellion     | 3   | Rival clan    |
| **3**  | Tavern    | 3   | Merchant          | 3   | Disappearance | 4   | Unnatural     |
| **4**  | Courtyard | 4   | Bandit            | 4   | War           | 5   | Negligence    |
| **5**  | Garden    | 5   | Herbalist         | 5   | Evacuation    | 6-7 | Bandits       |
| **6**  | Prison    | 6   | Ronin             | 6   | Murder        | 8   | The People    |
| **7**  | Shrine    | 7   | Fisherman         | 7   | Theft         | 9   | Corrupt ruler |
| **8**  | Bathhouse | 8   | Farmer            | 8   | Kidnap        | 10  | Outsiders     |
| **9**  | Armory    | 9   | Stranger          | 9   | Mystery       |     |               |
| **10** | Port      | 10  | Daimyo’s Emissary | 10  | Feud          |     |               |

<!-- Feudal Japan RPG Hook Generator -->
<style>
#hook-gen { font-family: system-ui, sans-serif; padding: 1.25rem 0; }
#hook-gen button { font-size: 15px; padding: 9px 22px; cursor: pointer; border: 1px solid #aaa; border-radius: 8px; background: #fff; }
#hook-gen button:hover { background: #f5f5f5; }
#hook-gen .result-block { background: #f8f7f4; border: 1px solid #ddd; border-radius: 10px; padding: 1.1rem 1.4rem; margin: 1.1rem 0; min-height: 58px; }
#hook-gen .hook-text { font-size: 15px; line-height: 1.75; margin: 0; color: #1a1a1a; }
#hook-gen .hook-text b.loc { color: #0F6E56; }
#hook-gen .hook-text b.contact { color: #533ab7; }
#hook-gen .hook-text b.event { color: #993c1d; }
#hook-gen .hook-text b.cause { color: #854f0b; }
#hook-gen .roll-tag { display: inline-block; font-size: 10px; padding: 1px 6px; border-radius: 6px; margin-left: 4px; vertical-align: middle; font-weight: normal; }
#hook-gen .rt-loc { background: #E1F5EE; color: #085041; }
#hook-gen .rt-contact { background: #EEEDFE; color: #3C3489; }
#hook-gen .rt-event { background: #FAECE7; color: #712B13; }
#hook-gen .rt-cause { background: #FAEEDA; color: #633806; }
#hook-gen .table-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin-top: 1rem; }
#hook-gen .col-card { border: 1px solid #ddd; border-radius: 8px; overflow: hidden; font-size: 12px; }
#hook-gen .col-header { padding: 5px 9px; font-size: 11px; font-weight: 600; text-align: center; }
#hook-gen .h-loc { background: #E1F5EE; color: #085041; }
#hook-gen .h-contact { background: #EEEDFE; color: #3C3489; }
#hook-gen .h-event { background: #FAECE7; color: #712B13; }
#hook-gen .h-cause { background: #FAEEDA; color: #633806; }
#hook-gen .col-body { padding: 6px 9px; }
#hook-gen .row { display: flex; gap: 6px; padding: 2px 0; color: #555; }
#hook-gen .row .n { min-width: 20px; font-size: 10px; color: #aaa; }
#hook-gen .row .v { color: #222; }
#hook-gen .row.hi .n, #hook-gen .row.hi .v { font-weight: 700; color: #1a1a1a; }
@media (max-width: 480px) { #hook-gen .table-grid { grid-template-columns: repeat(2, 1fr); } }
</style>

<div id="hook-gen">
  <button onclick="hgGenerate()">&#x2684; Roll the hook</button>
  <div class="result-block" id="hg-output">
    <p style="font-size:13px;color:#999;margin:0;">Press the button to generate a scenario hook.</p>
  </div>
  <div class="table-grid" id="hg-tables"></div>
</div>

<script>
(function(){
  var loc  = [[1,"Market"],[2,"Tea House"],[3,"Tavern"],[4,"Courtyard"],[5,"Garden"],[6,"Prison"],[7,"Shrine"],[8,"Bathhouse"],[9,"Armory"],[10,"Port"]];
  var con  = [[1,"Village Elder"],[2,"Monk"],[3,"Merchant"],[4,"Bandit"],[5,"Herbalist"],[6,"Ronin"],[7,"Fisherman"],[8,"Farmer"],[9,"Stranger"],[10,"Daimyo's Emissary"]];
  var evt  = [[1,"Plague"],[2,"Rebellion"],[3,"Disappearance"],[4,"War"],[5,"Evacuation"],[6,"Murder"],[7,"Theft"],[8,"Kidnap"],[9,"Mystery"],[10,"Feud"]];
  var causeRows = [[[1,2],"Monsters"],[[3],"Rival clan"],[[4],"Unnatural"],[[5],"Negligence"],[[6,7],"Bandits"],[[8],"The People"],[[9],"Corrupt ruler"],[[10],"Outsiders"]];
  var causeFlat = [];
  causeRows.forEach(function(r){ r[0].forEach(function(n){ causeFlat[n]=r[1]; }); });

  function d(n){ return Math.floor(Math.random()*n)+1; }
  function find(t,n){ for(var i=0;i<t.length;i++) if(t[i][0]===n) return t[i][1]; }

  window.hgGenerate = function(){
    var lr=d(10), cr=d(10), er=d(10), ur=d(10);
    document.getElementById("hg-output").innerHTML =
      '<p class="hook-text">The players meet in a <b class="loc">'+find(loc,lr)+'</b><span class="roll-tag rt-loc">'+lr+'</span> with <b class="contact">'+find(con,cr)+'</b><span class="roll-tag rt-contact">'+cr+'</span> who speaks of <b class="event">'+find(evt,er)+'</b><span class="roll-tag rt-event">'+er+'</span> caused by <b class="cause">'+causeFlat[ur]+'</b><span class="roll-tag rt-cause">'+ur+'</span>.</p>';

    var cols = [
      {cls:"loc",  hcls:"h-loc",  label:"Location (d10)",  data:loc,  roll:lr},
      {cls:"con",  hcls:"h-contact",label:"Contact (d10)", data:con,  roll:cr},
      {cls:"evt",  hcls:"h-event", label:"Event (d10)",    data:evt,  roll:er},
      {cls:"cause",hcls:"h-cause", label:"Cause (d10)",    data:null, roll:ur}
    ];
    var html="";
    cols.forEach(function(col){
      html+='<div class="col-card"><div class="col-header '+col.hcls+'">'+col.label+'</div><div class="col-body">';
      if(col.data){
        col.data.forEach(function(r){
          html+='<div class="row'+(r[0]===col.roll?' hi':'')+'"><span class="n">'+r[0]+'</span><span class="v">'+r[1]+'</span></div>';
        });
      } else {
        causeRows.forEach(function(r){
          var hi=r[0].indexOf(col.roll)>-1;
          var lbl=r[0].length>1?r[0][0]+'-'+r[0][r[0].length-1]:r[0][0];
          html+='<div class="row'+(hi?' hi':'')+'"><span class="n">'+lbl+'</span><span class="v">'+r[1]+'</span></div>';
        });
      }
      html+='</div></div>';
    });
    document.getElementById("hg-tables").innerHTML=html;
  };
})();
</script>
<!-- End Hook Generator -->

### Players must go to \[ADJECTIVE\] \[LOCATION\] and \[ACTION\].

| D20 | ADJECTIVE | D20 | ADJECTIVE | D20 | LOCATION | D20 | LOCATION | D10 | ACTION |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| **1** | Ancient | 11 | Radiant | 1 | Shrine | 11 | Tomb | 1 | Capture foe |
| **2** | Sacred | 12 | Shadowy | 2 | Cave | 12 | Cliffside | 2 | Defeat an enemy |
| **3** | Forbidden | 13 | Frosted | 3 | Temple | 13 | Island | 3 | Rescue a captive |
| **4** | Hidden | 14 | Ornate | 4 | Grove | 14 | Mountain | 4 | Gather intelligence |
| **5** | Mystical | 15 | Crumbling | 5 | Fortress | 15 | Pass | 5 | Win contest |
| **6** | Cursed | 16 | Verdant | 6 | Battlefield | 16 | Garden | 6 | Act as escort |
| **7** | Celestial | 17 | Obsidian | 7 | Waterfall | 17 | Ruins | 7 | Deliver a message |
| **8** | Haunted | 18 | Crimson | 8 | Village | 18 | Riverbank | 8 | Negotiate |
| **9** | Shimmering | 19 | Legendary | 9 | Forest | 19 | Hot Springs | 9 | Perform a ritual |
| **10** | Ethereal | 20 | Blessed | 10 | Lake | 20 | Pagoda | 10 | Find item (roll Adjective/Item Table) |

<!-- Feudal Japan RPG Mission Generator -->
<style>
#mg { font-family: system-ui, sans-serif; padding: 1.25rem 0; }
#mg button { font-size: 15px; padding: 9px 22px; cursor: pointer; border: 1px solid #aaa; border-radius: 8px; background: #fff; }
#mg button:hover { background: #f5f5f5; }
#mg .result-block { background: #f8f7f4; border: 1px solid #ddd; border-radius: 10px; padding: 1.1rem 1.4rem; margin: 1.1rem 0; min-height: 58px; }
#mg .hook-text { font-size: 15px; line-height: 1.75; margin: 0; color: #1a1a1a; }
#mg .hook-text b.adj { color: #533ab7; }
#mg .hook-text b.loc { color: #0F6E56; }
#mg .hook-text b.act { color: #993c1d; }
#mg .roll-tag { display: inline-block; font-size: 10px; padding: 1px 6px; border-radius: 6px; margin-left: 4px; vertical-align: middle; font-weight: normal; }
#mg .rt-adj { background: #EEEDFE; color: #3C3489; }
#mg .rt-loc { background: #E1F5EE; color: #085041; }
#mg .rt-act { background: #FAECE7; color: #712B13; }
#mg .note { font-size: 13px; color: #666; margin: 0.5rem 0 0; }
#mg .table-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-top: 1rem; }
#mg .col-card { border: 1px solid #ddd; border-radius: 8px; overflow: hidden; font-size: 12px; }
#mg .col-header { padding: 5px 9px; font-size: 11px; font-weight: 600; text-align: center; }
#mg .h-adj { background: #EEEDFE; color: #3C3489; }
#mg .h-loc { background: #E1F5EE; color: #085041; }
#mg .h-act { background: #FAECE7; color: #712B13; }
#mg .col-body { padding: 6px 9px; }
#mg .row { display: flex; gap: 6px; padding: 2px 0; color: #555; }
#mg .row .n { min-width: 22px; font-size: 10px; color: #aaa; }
#mg .row .v { color: #222; }
#mg .row.hi .n, #mg .row.hi .v { font-weight: 700; color: #1a1a1a; }
@media (max-width: 480px) { #mg .table-grid { grid-template-columns: 1fr; } }
</style>

<div id="mg">
  <button onclick="mgGen()">&#x2684; Roll the mission</button>
  <div class="result-block" id="mg-out">
    <p style="font-size:13px;color:#999;margin:0;">Press the button to generate a mission.</p>
  </div>
  <div class="table-grid" id="mg-tables"></div>
</div>

<script>
(function(){
  var adj = [[1,"Ancient"],[2,"Sacred"],[3,"Forbidden"],[4,"Hidden"],[5,"Mystical"],[6,"Cursed"],[7,"Celestial"],[8,"Haunted"],[9,"Shimmering"],[10,"Ethereal"],[11,"Radiant"],[12,"Shadowy"],[13,"Frosted"],[14,"Ornate"],[15,"Crumbling"],[16,"Verdant"],[17,"Obsidian"],[18,"Crimson"],[19,"Legendary"],[20,"Blessed"]];
  var loc = [[1,"Shrine"],[2,"Cave"],[3,"Temple"],[4,"Grove"],[5,"Fortress"],[6,"Battlefield"],[7,"Waterfall"],[8,"Village"],[9,"Forest"],[10,"Lake"],[11,"Tomb"],[12,"Cliffside"],[13,"Island"],[14,"Mountain"],[15,"Pass"],[16,"Garden"],[17,"Ruins"],[18,"Riverbank"],[19,"Hot Springs"],[20,"Pagoda"]];
  var act = [[1,"Capture a foe"],[2,"Defeat an enemy"],[3,"Rescue a captive"],[4,"Gather intelligence"],[5,"Win a contest"],[6,"Act as escort"],[7,"Deliver a message"],[8,"Negotiate"],[9,"Perform a ritual"],[10,"Find an item (roll Adjective/Item table)"]];

  function d(n){ return Math.floor(Math.random()*n)+1; }
  function find(t,n){ for(var i=0;i<t.length;i++) if(t[i][0]===n) return t[i][1]; return "?"; }

  window.mgGen = function(){
    var ar=d(20), lr=d(20), acr=d(10);
    var adjVal=find(adj,ar), locVal=find(loc,lr), actVal=find(act,acr);
    var isFind = acr===10;
    var note = isFind ? '<p class="note">&#x2605; Roll on the Adjective/Item table to determine what must be found.</p>' : '';
    document.getElementById("mg-out").innerHTML =
      '<p class="hook-text">Players must go to <b class="adj">'+adjVal+'</b><span class="roll-tag rt-adj">'+ar+'</span> <b class="loc">'+locVal+'</b><span class="roll-tag rt-loc">'+lr+'</span> and <b class="act">'+actVal+'</b><span class="roll-tag rt-act">'+acr+'</span>.</p>'+note;

    var cols=[
      {hcls:"h-adj",label:"Adjective (d20)",data:adj,roll:ar},
      {hcls:"h-loc",label:"Location (d20)",data:loc,roll:lr},
      {hcls:"h-act",label:"Action (d10)",data:act,roll:acr}
    ];
    var html="";
    cols.forEach(function(col){
      html+='<div class="col-card"><div class="col-header '+col.hcls+'">'+col.label+'</div><div class="col-body">';
      col.data.forEach(function(r){
        html+='<div class="row'+(r[0]===col.roll?' hi':'')+'"><span class="n">'+r[0]+'</span><span class="v">'+r[1]+'</span></div>';
      });
      html+='</div></div>';
    });
    document.getElementById("mg-tables").innerHTML=html;
  };
})();
</script>
<!-- End Mission Generator -->

### Adjective/Item (2D20)

| D20    | ADJECTIVE | D20 | ADJECTIVE  | D20 | ITEM          | D20 | ITEM    |
|:-------|:----------|:----|:-----------|:----|:--------------|:----|:--------|
| **1**  | Ancient   | 11  | Forbidden  | 1   | Plague        | 11  | Toolkit |
| **2**  | Sacred    | 12  | Celestial  | 2   | Rebellion     | 12  | Lantern |
| **3**  | Mystical  | 13  | Shadowy    | 3   | Disappearance | 13  | Edict   |
| **4**  | Enchanted | 14  | Radiant    | 4   | War           | 14  | Scale   |
| **5**  | Legendary | 15  | Phantom    | 5   | Evacuation    | 15  | Flute   |
| **6**  | Cursed    | 16  | Worn       | 6   | Murder        | 16  | Mask    |
| **7**  | Ornate    | 17  | Shimmering | 7   | Theft         | 17  | Branch  |
| **8**  | Blessed   | 18  | Obsidian   | 8   | Kidnap        | 18  | Banner  |
| **9**  | Hidden    | 19  | Frosted    | 9   | Mystery       | 19  | Statue  |
| **10** | Ethereal  | 20  | Crimson    | 10  | Feud          | 20  | Pearl   |

<!-- Adjective / Item Generator -->
<style>
#adji-gen { font-family: var(--font-sans); padding: 1.5rem 0; }
#adji-gen button { font-size: 15px; padding: 9px 22px; cursor: pointer; border: 1px solid #aaa; border-radius: 8px; background: #fff; }
#adji-gen .result-block { background: var(--color-background-secondary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-lg); padding: 1.25rem 1.5rem; margin: 1.25rem 0; min-height: 64px; }
#adji-gen .hook-text { font-size: 16px; line-height: 1.7; color: var(--color-text-primary); }
#adji-gen .hook-text span { font-weight: 500; }
#adji-gen .adj { color: #533ab7; }
#adji-gen .item { color: #0F6E56; }
#adji-gen .table-grid { display: grid; grid-template-columns: repeat(2, minmax(0,1fr)); gap: 12px; margin-top: 1.25rem; }
#adji-gen .col-card { border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-md); overflow: hidden; }
#adji-gen .col-header { padding: 6px 10px; font-size: 12px; font-weight: 500; letter-spacing: 0.02em; text-align: center; }
#adji-gen .col-header.adj { background: #EEEDFE; color: #3C3489; }
#adji-gen .col-header.item { background: #E1F5EE; color: #085041; }
#adji-gen .col-body { padding: 8px 10px; }
#adji-gen .col-body div { font-size: 12px; color: var(--color-text-secondary); padding: 2px 0; display: flex; gap: 6px; }
#adji-gen .col-body div span.num { color: var(--color-text-tertiary); min-width: 22px; font-size: 11px; }
#adji-gen .col-body div span.val { color: var(--color-text-primary); }
#adji-gen .col-body div.highlight span.val { font-weight: 500; }
#adji-gen .col-body div.highlight span.num { font-weight: 500; }
#adji-gen .roll-tag { display: inline-block; font-size: 11px; padding: 2px 8px; border-radius: var(--border-radius-md); margin-left: 6px; vertical-align: middle; }
#adji-gen .roll-tag.adj { background: #EEEDFE; color: #3C3489; }
#adji-gen .roll-tag.item { background: #E1F5EE; color: #085041; }
@media (max-width: 520px) { #adji-gen .table-grid { grid-template-columns: 1fr; } }
</style>

<div id="adji-gen">
  <button id="adji-btn" onclick="adjiGenerate()" style="font-size: 15px; padding: 10px 24px; cursor: pointer;">Roll adjective / item</button>
  <div class="result-block" id="adji-output">
    <p style="font-size: 14px; color: var(--color-text-tertiary); margin: 0;">Press the button to generate an adjective and item.</p>
  </div>
  <div class="table-grid" id="adji-tables"></div>
</div>

<script>
const adjiTables = {
  adjective: [
    [1,"Ancient"],[2,"Sacred"],[3,"Mystical"],[4,"Enchanted"],[5,"Legendary"],
    [6,"Cursed"],[7,"Ornate"],[8,"Blessed"],[9,"Hidden"],[10,"Ethereal"],
    [11,"Forbidden"],[12,"Celestial"],[13,"Shadowy"],[14,"Radiant"],[15,"Phantom"],
    [16,"Worn"],[17,"Shimmering"],[18,"Obsidian"],[19,"Frosted"],[20,"Crimson"]
  ],
  item: [
    [1,"Plague"],[2,"Rebellion"],[3,"Disappearance"],[4,"War"],[5,"Evacuation"],
    [6,"Murder"],[7,"Theft"],[8,"Kidnap"],[9,"Mystery"],[10,"Feud"],
    [11,"Toolkit"],[12,"Lantern"],[13,"Edict"],[14,"Scale"],[15,"Flute"],
    [16,"Mask"],[17,"Branch"],[18,"Banner"],[19,"Statue"],[20,"Pearl"]
  ]
};

function adjiRoll(n) { return Math.floor(Math.random() * n) + 1; }

let adjiLast = {};

function adjiGenerate() {
  const adjRoll = adjiRoll(20);
  const itemRoll = adjiRoll(20);
  adjiLast = { adjRoll, itemRoll };

  const adj = adjiTables.adjective.find(r => r[0] === adjRoll)[1];
  const item = adjiTables.item.find(r => r[0] === itemRoll)[1];

  document.getElementById("adji-output").innerHTML = `
    <p class="hook-text">
      <span class="adj">${adj}</span>
      <span class="roll-tag adj">${adjRoll}</span>
      <span class="item">${item}</span>
      <span class="roll-tag item">${itemRoll}</span>.
    </p>`;

  adjiRenderTables();
}

function adjiRenderTables() {
  const cols = [
    { key: "adj", label: "Adjective (d20)", data: adjiTables.adjective, roll: adjiLast.adjRoll },
    { key: "item", label: "Item (d20)", data: adjiTables.item, roll: adjiLast.itemRoll }
  ];

  let html = "";
  cols.forEach(col => {
    html += `<div class="col-card"><div class="col-header ${col.key}">${col.label}</div><div class="col-body">`;
    col.data.forEach(([num, val]) => {
      const hi = num === col.roll ? " highlight" : "";
      html += `<div class="${hi}"><span class="num">${num}</span><span class="val">${val}</span></div>`;
    });
    html += `</div></div>`;
  });

  document.getElementById("adji-tables").innerHTML = html;
}
</script>
<!-- End Adjective / Item Generator -->

### Scenario Example

The players meet in a village (9) **Armory** with a (9) **Stranger** who speaks of (6) **Murder**, possibly caused by a (3) **Rival Clan**. Players must go to the (8/14) **Haunted Mountain** and (10) **Find the** (11/2) **Forbidden Scroll**.

## Factions

A region is typically dominated by one or more factions, each with their own unique Perks, Agenda, and Obstacles. Smaller regions should have 1-2 factions, while larger regions could have as many as 5-6 factions.

### Faction Type (D20)

| D20 | TYPE      | D20 | TYPE           | D20 | TYPE            | D20 | TYPE     |
|:----|:----------|:----|:---------------|:----|:----------------|:----|:---------|
| 1   | Artisans  | 6   | Explorers      | 11  | Nomads          | 16  | Rulers   |
| 2   | Commoners | 7   | Industrialists | 12  | Pilgrims        | 17  | Scholars |
| 3   | Criminals | 8   | Merchants      | 13  | Protectors      | 18  | Settlers |
| 4   | Cultists  | 9   | Military       | 14  | Religious       | 19  | Spies    |
| 5   | Exiles    | 10  | Nobles         | 15  | Revolutionaries | 20  | Tribe    |

### Faction and Leader Traits

Each Faction has one trait for itself and one trait associated with its Leader. Roll d20 and then d20 for each. Reroll any repeat results.

| 1-10 |               |     |               | 11-20 |              |     |            |
|:-----|---------------|-----|---------------|:------|--------------|-----|------------|
| D20  | Trait         | D20 | Trait         | D20   | Trait        | D20 | Trait      |
| 1    | Bankrupt      | 11  | Disciplined   | 1     | Intellectual | 11  | Ruthless   |
| 2    | Cautious      | 12  | Efficient     | 2     | Lawless      | 12  | Secret     |
| 3    | Charitable    | 13  | Enigmatic     | 3     | Manipulative | 13  | Shrewd     |
| 4    | Cold          | 14  | Expanding     | 4     | Martial      | 14  | Stealthy   |
| 5    | Collaborative | 15  | Generous      | 5     | Mercurial    | 15  | Strong     |
| 6    | Connected     | 16  | Greedy        | 6     | Pious        | 16  | Stubborn   |
| 7    | Corrupt       | 17  | Honorable     | 7     | Popular      | 17  | Suspicious |
| 8    | Cruel         | 18  | Hot Tempered  | 8     | Proud        | 18  | Threatened |
| 9    | Decadent      | 19  | Incompetent   | 9     | Resourceful  | 19  | Vengeful   |
| 10   | Devious       | 20  | Incorruptible | 10    | Righteous    | 20  | Xenophobic |

### Faction Agents (D20)

Agents are often in charge of completing one or more of the goals of the agenda of a faction. Particularly large factions may have additional agents, each in charge of a distinct goal. Agents may have personal motivations that differ from the faction’s main agenda, a fact that canny PCs can exploit for their own gain.

| D20 | AGENT      | D20 | AGENT         | D20 | AGENT     | D20 | AGENT      |
|:----|:-----------|:----|:--------------|:----|:----------|:----|:-----------|
| 1   | Academic   | 6   | Gravedigger   | 11  | Lord      | 16  | Peddler    |
| 2   | Assassin   | 7   | Guard/Soldier | 12  | Merchant  | 17  | Politician |
| 3   | Blacksmith | 8   | Healer        | 13  | Monk      | 18  | Spy        |
| 4   | Farmer     | 9   | Jailer        | 14  | Mystic    | 19  | Thief      |
| 5   | General    | 10  | Laborer       | 15  | Outlander | 20  | Thug       |

### Faction Perks

Factions possess perks that assist them in accomplishing their agenda. Perks reflect a faction’s influence, materials, wealth, and other unique features. Factions leverage their perks as much as possible when trying to achieve their goals, and at the same time continually work to acquire more perks.

Roll d20 for the number of perks the faction has, then roll d20 again for the types of perks. Reroll repeated results.

| NUMBER OF PERKS (D20) |     |          |     |           |     |           |     |
|:----------------------|-----|----------|-----|-----------|-----|-----------|-----|
| 1-7                   | 2   | **8-12** | 2   | **13-17** | 3   | **18-20** | 4   |

| D20    | PERK        | D20 | PERK           |
|:-------|:------------|:----|:---------------|
| **1**  | Alliances   | 11  | Magic          |
| **2**  | Anonymity   | 12  | Members        |
| **3**  | Apparatus   | 13  | Popularity     |
| **4**  | Beliefs     | 14  | Position       |
| **5**  | Charisma    | 15  | Renown         |
| **6**  | Conviction  | 16  | Resources      |
| **7**  | Fealty      | 17  | Ruthlessness   |
| **8**  | Force       | 18  | Specialization |
| **9**  | Information | 19  | Subterfuge     |
| **10** | Lineage     | 20  | Wealth         |

### Faction Agendas

Factions will work to complete their agendas independently, enlisting the help of PCs when that would strengthen their agenda. Agendas are defined by a series of 3-5 Goals that build toward a clear objective. Goals are progressive, building on previous successes (or failures).

Goals should focus on acquiring a distinct advantage in order to proceed to the next goal. All factions have at least one obstacle that stands in the way of their completion. At least one goal should deal with the faction’s primary obstacle. Additional obstacles can arise through faction actions or through developments in the fiction.

Completing a faction’s agendas should be a significant event, potentially changing the political or natural landscape of a region.

Roll d20 for each column and combine.

| D20 | AGENDA | OBSTACLE |
|:---|:---|:---|
| **1** | Acquire assets/wealth | A geographic barrier or impassable terrain. |
| **2** | Control | A key piece of information must first be discovered. |
| **3** | Defeat or destroy faction/leader | A particular object or Relic is required. |
| **4** | Enrich members | A powerful figure or foe must be eliminated. |
| **5** | Exchange goods | Many must die, either as necessity or consequence. |
| **6** | Fame/Glory | A serious debt forces the faction to make dire choices. |
| **7** | Forge an alliance | A well-known prophecy predicts imminent failure. |
| **8** | Infiltrate faction | An alliance with an enemy must first be brokered. |
| **9** | Map the wild | An internal schism threatens to tear faction apart. |
| **10** | Overthrow order | Another faction has the same goal. |
| **11** | Preserve lineage/lore | Another faction stands in opposition. |
| **12** | Preserve the status quo/order | Vassals stand openly in opposition. |
| **13** | Produce goods | Considerable capital is required. |
| **14** | Protect/Reveal a secret | Hindered by cultural taboos. |
| **15** | Protect/defend themselves/something else | Contravenes an established code, with a heavy penalty. |
| **16** | Purge/eliminate traitors and/or competition | A rare but necessary resource must first be acquired |
| **17** | Revenge against a faction/leader | Must be carried out at a rare or exact moment. |
| **18** | Sell services/goods | Must be carried out in absolute secrecy. |
| **19** | Share knowledge/beliefs | Requires a specialist of an uncommon sort. |
| **20** | Survive | The outcome would lead to unavoidable conflict. |

<!-- Faction Generator -->
<style>
#faction-gen { font-family: var(--font-sans); padding: 1.5rem 0; }
#hook-gen button { font-size: 15px; padding: 9px 22px; cursor: pointer; border: 1px solid #aaa; border-radius: 8px; background: #fff; }
#faction-gen .result-block { background: var(--color-background-secondary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-lg); padding: 1.25rem 1.5rem; margin: 1.25rem 0; min-height: 64px; }
#faction-gen .hook-text { font-size: 16px; line-height: 1.8; color: var(--color-text-primary); }
#faction-gen .hook-text span { font-weight: 500; }
#faction-gen .type { color: #0F6E56; }
#faction-gen .trait { color: #533ab7; }
#faction-gen .leader { color: #712B13; }
#faction-gen .agent { color: #854f0b; }
#faction-gen .perk { color: #085041; }
#faction-gen .agenda { color: #3C3489; }
#faction-gen .obstacle { color: #712B13; }
#faction-gen .table-grid { display: grid; grid-template-columns: repeat(4, minmax(0,1fr)); gap: 12px; margin-top: 1.25rem; }
#faction-gen .col-card { border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-md); overflow: hidden; }
#faction-gen .col-header { padding: 6px 10px; font-size: 12px; font-weight: 500; letter-spacing: 0.02em; text-align: center; }
#faction-gen .col-header.type { background: #E1F5EE; color: #085041; }
#faction-gen .col-header.trait { background: #EEEDFE; color: #3C3489; }
#faction-gen .col-header.agent { background: #FAECE7; color: #712B13; }
#faction-gen .col-header.perk { background: #FAEEDA; color: #633806; }
#faction-gen .col-body { padding: 8px 10px; }
#faction-gen .col-body div { font-size: 12px; color: var(--color-text-secondary); padding: 2px 0; display: flex; gap: 6px; }
#faction-gen .col-body div span.num { color: var(--color-text-tertiary); min-width: 22px; font-size: 11px; }
#faction-gen .col-body div span.val { color: var(--color-text-primary); }
#faction-gen .col-body div.highlight span.val { font-weight: 500; }
#faction-gen .col-body div.highlight span.num { font-weight: 500; }
#faction-gen .roll-tag { display: inline-block; font-size: 11px; padding: 2px 8px; border-radius: var(--border-radius-md); margin-left: 6px; vertical-align: middle; }
#faction-gen .roll-tag.type { background: #E1F5EE; color: #085041; }
#faction-gen .roll-tag.trait { background: #EEEDFE; color: #3C3489; }
#faction-gen .roll-tag.agent { background: #FAECE7; color: #712B13; }
#faction-gen .roll-tag.perk { background: #FAEEDA; color: #633806; }
#faction-gen ul { margin: 0.5rem 0 0 1.25rem; padding: 0; }
#faction-gen li { margin: 0.2rem 0; }
@media (max-width: 900px) { #faction-gen .table-grid { grid-template-columns: repeat(2, minmax(0,1fr)); } }
@media (max-width: 520px) { #faction-gen .table-grid { grid-template-columns: 1fr; } }
</style>

<div id="faction-gen">
  <button id="faction-btn" onclick="generateFaction()" style="font-size: 15px; padding: 10px 24px; cursor: pointer;">Generate faction</button>
  <div class="result-block" id="faction-output">
    <p style="font-size: 14px; color: var(--color-text-tertiary); margin: 0;">Press the button to generate a faction from all faction tables.</p>
  </div>
  <div class="table-grid" id="faction-tables"></div>
</div>

<script>
const factionTables = {
  type: [
    [1,"Artisans"],[2,"Commoners"],[3,"Criminals"],[4,"Cultists"],[5,"Exiles"],
    [6,"Explorers"],[7,"Industrialists"],[8,"Merchants"],[9,"Military"],[10,"Nobles"],
    [11,"Nomads"],[12,"Pilgrims"],[13,"Protectors"],[14,"Religious"],[15,"Revolutionaries"],
    [16,"Rulers"],[17,"Scholars"],[18,"Settlers"],[19,"Spies"],[20,"Tribe"]
  ],
  factionTrait: [
    [1,"Bankrupt"],[2,"Cautious"],[3,"Charitable"],[4,"Cold"],[5,"Collaborative"],
    [6,"Connected"],[7,"Corrupt"],[8,"Cruel"],[9,"Decadent"],[10,"Devious"],
    [11,"Disciplined"],[12,"Efficient"],[13,"Enigmatic"],[14,"Expanding"],[15,"Generous"],
    [16,"Greedy"],[17,"Honorable"],[18,"Hot Tempered"],[19,"Incompetent"],[20,"Incorruptible"]
  ],
  leaderTrait: [
    [1,"Intellectual"],[2,"Lawless"],[3,"Manipulative"],[4,"Martial"],[5,"Mercurial"],
    [6,"Pious"],[7,"Popular"],[8,"Proud"],[9,"Resourceful"],[10,"Righteous"],
    [11,"Ruthless"],[12,"Secret"],[13,"Shrewd"],[14,"Stealthy"],[15,"Strong"],
    [16,"Stubborn"],[17,"Suspicious"],[18,"Threatened"],[19,"Vengeful"],[20,"Xenophobic"]
  ],
  agent: [
    [1,"Academic"],[2,"Assassin"],[3,"Blacksmith"],[4,"Farmer"],[5,"General"],
    [6,"Gravedigger"],[7,"Guard/Soldier"],[8,"Healer"],[9,"Jailer"],[10,"Laborer"],
    [11,"Lord"],[12,"Merchant"],[13,"Monk"],[14,"Mystic"],[15,"Outlander"],
    [16,"Peddler"],[17,"Politician"],[18,"Spy"],[19,"Thief"],[20,"Thug"]
  ],
  perkCount: [
    [[1,2,3,4,5,6,7],2],
    [[8,9,10,11,12],2],
    [[13,14,15,16,17],3],
    [[18,19,20],4]
  ],
  perk: [
    [1,"Alliances"],[2,"Anonymity"],[3,"Apparatus"],[4,"Beliefs"],[5,"Charisma"],
    [6,"Conviction"],[7,"Fealty"],[8,"Force"],[9,"Information"],[10,"Lineage"],
    [11,"Magic"],[12,"Members"],[13,"Popularity"],[14,"Position"],[15,"Renown"],
    [16,"Resources"],[17,"Ruthlessness"],[18,"Specialization"],[19,"Subterfuge"],[20,"Wealth"]
  ],
  agenda: [
    [1,"Acquire assets/wealth"],[2,"Control"],[3,"Defeat or destroy faction/leader"],[4,"Enrich members"],[5,"Exchange goods"],
    [6,"Fame/Glory"],[7,"Forge an alliance"],[8,"Infiltrate faction"],[9,"Map the wild"],[10,"Overthrow order"],
    [11,"Preserve lineage/lore"],[12,"Preserve the status quo/order"],[13,"Produce goods"],[14,"Protect/Reveal a secret"],[15,"Protect/defend themselves/something else"],
    [16,"Purge/eliminate traitors and/or competition"],[17,"Revenge against a faction/leader"],[18,"Sell services/goods"],[19,"Share knowledge/beliefs"],[20,"Survive"]
  ],
  obstacle: [
    [1,"A geographic barrier or impassable terrain."],
    [2,"A key piece of information must first be discovered."],
    [3,"A particular object or Relic is required."],
    [4,"A powerful figure or foe must be eliminated."],
    [5,"Many must die, either as necessity or consequence."],
    [6,"A serious debt forces the faction to make dire choices."],
    [7,"A well-known prophecy predicts imminent failure."],
    [8,"An alliance with an enemy must first be brokered."],
    [9,"An internal schism threatens to tear faction apart."],
    [10,"Another faction has the same goal."],
    [11,"Another faction stands in opposition."],
    [12,"Vassals stand openly in opposition."],
    [13,"Considerable capital is required."],
    [14,"Hindered by cultural taboos."],
    [15,"Contravenes an established code, with a heavy penalty."],
    [16,"A rare but necessary resource must first be acquired."],
    [17,"Must be carried out at a rare or exact moment."],
    [18,"Must be carried out in absolute secrecy."],
    [19,"Requires a specialist of an uncommon sort."],
    [20,"The outcome would lead to unavoidable conflict."]
  ]
};

function factionRoll(n) { return Math.floor(Math.random() * n) + 1; }

function perkCountFromRoll(roll) {
  for (const [rolls, val] of factionTables.perkCount) {
    if (rolls.includes(roll)) return val;
  }
  return 2;
}

function uniqueRolls(max, count) {
  const picks = [];
  while (picks.length < count) {
    const r = factionRoll(max);
    if (!picks.includes(r)) picks.push(r);
  }
  return picks;
}

let factionLast = {};

function generateFaction() {
  const typeRoll = factionRoll(20);
  const factionTraitRoll = factionRoll(20);
  const leaderTraitRoll = factionRoll(20);
  const agentRoll = factionRoll(20);
  const perkCountRoll = factionRoll(20);
  const perkTotal = perkCountFromRoll(perkCountRoll);
  const perkRolls = uniqueRolls(20, perkTotal);
  const agendaRoll = factionRoll(20);
  const obstacleRoll = factionRoll(20);

  factionLast = {
    typeRoll, factionTraitRoll, leaderTraitRoll, agentRoll,
    perkCountRoll, perkRolls, agendaRoll, obstacleRoll
  };

  const type = factionTables.type.find(r => r[0] === typeRoll)[1];
  const factionTrait = factionTables.factionTrait.find(r => r[0] === factionTraitRoll)[1];
  const leaderTrait = factionTables.leaderTrait.find(r => r[0] === leaderTraitRoll)[1];
  const agent = factionTables.agent.find(r => r[0] === agentRoll)[1];
  const perks = perkRolls.map(r => factionTables.perk.find(p => p[0] === r)[1]);
  const agenda = factionTables.agenda.find(r => r[0] === agendaRoll)[1];
  const obstacle = factionTables.obstacle.find(r => r[0] === obstacleRoll)[1];

  document.getElementById("faction-output").innerHTML = `
    <div class="hook-text">
      <div>A Faction of 
        <span class="type">${type}</span>
        <span class="roll-tag type">${typeRoll}</span>
      </div>
      <div style="margin-top: 0.5rem;">
        Faction Trait: <span class="trait">${factionTrait}</span>
        <span class="roll-tag trait">${factionTraitRoll}</span><br>
        Leader Trait: <span class="leader">${leaderTrait}</span>
        <span class="roll-tag trait">${leaderTraitRoll}</span><br>
        Agent: <span class="agent">${agent}</span>
        <span class="roll-tag agent">${agentRoll}</span><br>
        Perks (${perkTotal}):
        <span class="perk">${perks.join(", ")}</span>
        <span class="roll-tag perk">${perkRolls.join(", ")}</span><br>
        Agenda: <span class="agenda">${agenda}</span>
        <span class="roll-tag trait">${agendaRoll}</span><br>
        Obstacle: <span class="obstacle">${obstacle}</span>
        <span class="roll-tag agent">${obstacleRoll}</span>
      </div>
    </div>`;

  renderFactionTables();
}

function renderFactionTables() {
  const cols = [
    { key: "type", label: "Faction Type (d20)", data: factionTables.type, roll: factionLast.typeRoll },
    { key: "trait", label: "Faction Trait (d20)", data: factionTables.factionTrait, roll: factionLast.factionTraitRoll },
    { key: "agent", label: "Leader Trait (d20)", data: factionTables.leaderTrait, roll: factionLast.leaderTraitRoll },
    { key: "perk", label: "Agent (d20)", data: factionTables.agent, roll: factionLast.agentRoll }
  ];

  let html = "";
  cols.forEach(col => {
    html += `<div class="col-card"><div class="col-header ${col.key}">${col.label}</div><div class="col-body">`;
    col.data.forEach(([num, val]) => {
      const hi = num === col.roll ? " highlight" : "";
      html += `<div class="${hi}"><span class="num">${num}</span><span class="val">${val}</span></div>`;
    });
    html += `</div></div>`;
  });

  html += `<div class="col-card"><div class="col-header perk">Perk Count / Perks</div><div class="col-body">`;
  factionTables.perkCount.forEach(([rolls, val]) => {
    const hi = rolls.includes(factionLast.perkCountRoll) ? " highlight" : "";
    const label = rolls.length > 1 ? `${rolls[0]}-${rolls[rolls.length-1]}` : `${rolls[0]}`;
    html += `<div class="${hi}"><span class="num">${label}</span><span class="val">${val} perks</span></div>`;
  });
  html += `<div style="height:8px;"></div>`;
  factionTables.perk.forEach(([num, val]) => {
    const hi = factionLast.perkRolls.includes(num) ? " highlight" : "";
    html += `<div class="${hi}"><span class="num">${num}</span><span class="val">${val}</span></div>`;
  });
  html += `</div></div>`;

  html += `<div class="col-card"><div class="col-header trait">Agenda (d20)</div><div class="col-body">`;
  factionTables.agenda.forEach(([num, val]) => {
    const hi = num === factionLast.agendaRoll ? " highlight" : "";
    html += `<div class="${hi}"><span class="num">${num}</span><span class="val">${val}</span></div>`;
  });
  html += `</div></div>`;

  html += `<div class="col-card"><div class="col-header agent">Obstacle (d20)</div><div class="col-body">`;
  factionTables.obstacle.forEach(([num, val]) => {
    const hi = num === factionLast.obstacleRoll ? " highlight" : "";
    html += `<div class="${hi}"><span class="num">${num}</span><span class="val">${val}</span></div>`;
  });
  html += `</div></div>`;

  document.getElementById("faction-tables").innerHTML = html;
}
</script>
<!-- End Faction Generator -->

### Example Faction

**Type:** Rulers: *Shihai Clan*. Disciplined, martial, stubborn.

**Perks: Conviction**: Firmly believe in their duty (and right) to lead the nation. **Position**: Traditionally observed as the leaders of the realm. **Wealth**: Their lands are among the most abundant throughout the nation.

**Agents:** (Lord) Shihai Daichi, heir to the Shihai daimyo title.

**Agenda:** Preserve order and reassert authority over the nation.

**Obstacles:** Opposed by other clans seeking authority.

### Faction Rules

The actions of the PCs can always overrule the necessity for a faction action, or in some cases shift the outcome of the roll in a favorable or unfavorable direction.

- By default, factions operate independent of the player character’s actions. If the PCs do nothing, the faction should still act to achieve their aims.

- The Guide should rely on the fiction to determine whether a faction is positioned to advance their agenda.

- Some goals may be time-sensitive or depend on explicit circumstances. Other times it might be more appropriate to introduce a new goal after a major event, alliance, or friction between one or more factions, etc.

- Whenever a faction is positioned to advance a goal in their agenda, roll a d6 on the **Faction Actions** table.

- If two factions are opposed, the faction most at risk makes a WIL save, using the score of its highest-ranking agent. On a fail, the faction does not roll on the **Faction Actions** table at this time.

#### Faction Actions (D6)

| D6    | CONSEQUENCE   | IMPACT                                            |
|:------|:--------------|:--------------------------------------------------|
| **1** | Major Success | A Goal is achieved and a new Advantage is found.  |
| **2** | Success       | A Goal is achieved, and no Perks are lost.        |
| **3** | Mixed Success | A Goal is achieved, but a Perk is lost.           |
| **4** | Status Quo    | Nothing is gained, but nothing is lost.           |
| **5** | Setback       | A Perk is lost.                                   |
| **6** | Failure       | A new Obstacle is introduced, and a Perk is lost. |

>**Pointcrawl or Hexcrawl?**
>Ikezu-ishi uses Cairn’s Wilderness Exploration rules which utilizes a pointcrawl system. The Guide may choose to use a hexcrawl or any other adventure system they’re comfortable with.

## Locations, Landmarks, and Encounters

When needed, the Guide can roll or choose locations and landmarks using the General or terrain specific tables. If a result does not fit the location or the story, the Guide may reroll or choose a location.

For each encounter table, the Guide may roll a D20 for encounters that include yokai. If playing a game or in a setting where there are no yokai, the Guide may roll a D12.

### General Terrain Features (D20)

| D20 | FEATURE |
|:---|:---|
| 1 | **Hidden Spring**: A freshwater spring hidden in the terrain. |
| 2 | **Vines**: An impassible tangle of throned vines blocks your path, forcing you to find another route. |
| 3 | **Sinkhole**: The earth opens up forming a gaping, seemingly bottomless hole. |
| 4 | **Quagmire**: A treacherous marshland filled with mud and water, difficult to traverse without sinking. |
| 5 | **Stone Path**: A well-worn path paved with smooth stones. |
| 6 | **Boulders**: Large rocks scattered across the landscape, offering cover or obstacles for travelers and adventurers. |
| 7 | **Bamboo Forest**: Dense stands of towering bamboo that create a labyrinthine network of paths. |
| 8 | **Clearing**: The land lays before you flat and open, no shade, no cover. |
| 9 | **Shrine**: A small, remote shrine that is unattended but well cared for. |
| 10 | **Ancient Tree**: A massive, old tree that stands out, with names and prayers carved into its bark. |
| 11 | **Mirror Lake**: A perfectly still lake that reflects the sky like a mirror. |
| 12 | **Ancient Canal**: The remains of a once-functional canal, now crumbling and overgrown. |
| 13 | **Well**: An old well where travelers leave offerings, hoping for granted wishes or blessings. |
| 14 | **Fog**: The land is mist-covered, reducing visibility and hiding dangers and treasures. |
| 15 | **Waterfall**: A tall waterfall crashes into a pool of clear water, perhaps concealing a cave. |
| 16 | **Echoing Canyon**: A deep canyon where sounds echo, making it hard to determine the source of noises. |
| 17 | **Cave Network**: An opening to a series of interconnected caves. |
| 18 | **Hot Springs**: Natural hot springs that locals believe have healing properties. |
| 19 | **Uncontrolled Fire**: A fire rages, billowing black smoke into the air and making it hard for travelers to breathe. |
| 20 | **Mossy Stone Garden**: An ancient garden overgrown with moss. |

### General Locations and Landmarks (D20)

<table style="width:99%;">
<colgroup>
<col style="width: 3%" />
<col style="width: 96%" />
</colgroup>
<thead>
<tr>
<th>D20</th>
<th>LOCATION OR LANDMARK</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td><strong>Haunted Ruins</strong>: The remains of an old structure that feels unnatural.</td>
</tr>
<tr>
<td>2</td>
<td><strong>Deserted Village</strong>: An old village that has been abandoned, with empty houses and overgrown paths.</td>
</tr>
<tr>
<td>3</td>
<td><strong>Zen Garden</strong>: A serene garden for contemplation and meditation, featuring carefully arranged rocks and gravel.</td>
</tr>
<tr>
<td>4</td>
<td><strong>Forgotten Cemetery</strong>: An old, overgrown cemetery with crumbling tombstones.</td>
</tr>
<tr>
<td>5</td>
<td><strong>Yokai Statue</strong>: As eerie sculpture depicting mythical creatures.</td>
</tr>
<tr>
<td>6</td>
<td><strong>Boardwalk Over Water Pit</strong>: A raised wooden pathway spanning over a pit filled with water.</td>
</tr>
<tr>
<td>7</td>
<td><strong>Ruined Torii Gate</strong>: The remains of a once grand torii gate which marked the entrance to a shrine, standing alone, overgrown with vines and moss.</td>
</tr>
<tr>
<td>8</td>
<td><strong>Orchard</strong>: A cultivated area where fruit trees are grown, providing food and natural beauty.</td>
</tr>
<tr>
<td>9</td>
<td><strong>Mysterious Monolith</strong>: A large, ancient stone with indecipherable carvings, standing alone in a field.</td>
</tr>
<tr>
<td>10</td>
<td><strong>Half Wall</strong>: A low wall constructed of stone or wood, marking property boundaries or providing minimal defense.</td>
</tr>
<tr>
<td>11</td>
<td><strong>Burnt Village</strong>: The charred remains of a village, possibly destroyed by war or natural disaster.</td>
</tr>
<tr>
<td>12</td>
<td><p><strong>Battlefield</strong>:</p>
<p>1-4: Past: The land lays strewn with the remains of soldiers.</p>
<p>5-6 Active: The sounds of armies crashing into each other are hard to mistake.</p></td>
</tr>
<tr>
<td>13</td>
<td><strong>Burial Mound</strong>: Ancient mounds containing the remains of the deceased.</td>
</tr>
<tr>
<td>14</td>
<td><strong>Minka House</strong> (A-Frame): A simple yet elegant farmhouse built with traditional architectural techniques. (Farm/Home)</td>
</tr>
<tr>
<td>15</td>
<td><strong>House</strong>: A traditional home where families live and survive. (Farm/Home)</td>
</tr>
<tr>
<td>16</td>
<td><strong>Dojo</strong>: A martial arts training facility where warriors hone their combat skills and discipline. (Estate)</td>
</tr>
<tr>
<td>17</td>
<td><strong>Tea House</strong>: Establishment where travelers can rest and socialize. (Town)</td>
</tr>
<tr>
<td>18</td>
<td><strong>Village</strong>: An established town with residents and merchants. (Town)</td>
</tr>
<tr>
<td>19</td>
<td><strong>Watch Tower</strong>: A fortified structure overlooking the surrounding landscape, providing strategic advantage and surveillance. (Market Town)</td>
</tr>
<tr>
<td>20</td>
<td><strong>Castle</strong>: A fortress serving as the residence of a lord and the seat of political power. (Castle Town)</td>
</tr>
</tbody>
</table>

### Coastal Locations and Landmarks (D12)

| D12 | LOCATION OR LANDMARK |
|:---|:---|
| 1 | **Fishermen's Wharf**: A lively dock where boats return with the day’s catch, surrounded by salty air and seagulls. |
| 2 | **Sunken Temple**: A half-submerged shrine only accessible during low tide, rumored to be guarded by sea spirits. |
| 3 | **Smuggler’s Cove**: A hidden cove beneath towering cliffs, used by pirates and smugglers to hide their illicit goods. |
| 4 | **Harbor Fortress**: A coastal fortress perched on a cliff. |
| 5 | **Tidal Flats**: A vast expanse of mud and sand exposed at low tide. |
| 6 | **Pearl Diver’s Hut**: A small village of pearl divers, known for their wealth. |
| 7 | **Stormbreaker Rock**: A jagged rock formation that juts out of the ocean, known for breaking mighty waves and ships. |
| 8 | **Salt Crystals Beach**: A beach where salt crystals glitter under the sun. |
| 9 | **Whale Graveyard**: A remote beach littered with the bones of enormous sea creatures. |
| 10 | **Seaside Market**: A busy coastal bazaar where traders from far lands barter spices, silks, and strange sea creatures. |
| 11 | **The Singing Cliffs**: Tall cliffs along the coast that produce an eerie, melodic hum when the wind blows through hidden crevices. |
| 12 | **Foghorn Tavern**: A rowdy tavern near the docks where sailors share tales of sea monsters and strange islands. |

### Coastal Encounters (D12 or D20)

| D12/20 | ENCOUNTER |
|:---|:---|
| 1 | A **Bandit** and 2 **Hunting Dogs** scour the beach, hunting for the entrance to a sea cave marked on a crude map. |
| 2-3 | D6 **Ashigaru** are on a quest to retrieve their fallen comrade. |
| 4-5 | As the party stops to consider an abandoned rowing boat bobs gently in the water, d4 **Kaizoku** jump out of the nearby foliage. |
| 6 | Beneath leaden skies, rain pelts relentlessly, soaking everything in its path. If players wish to continue travel, they must DEX save, if they fail, they lose 1 WIL. |
| 7 | Visibility diminishes as a mist shrouds the surroundings in an eerie haze. If players wish to continue travel, they must WIL save, if they fail, they become lost and lose 2 Watch before the fog lifts. If they make camp for the day the fog lifts by morning. |
| 8 | The path turns muddy, soon two feet deep a tough to travel. Water in ditches bubbles, ominous signs of impending danger. If players wish to continue travel, they must DEX save, if they fail, they become bogged down and lose 1 Watch. |
| 9-10 | The party stumbles upon a desolate village, its charred remnants hinting at a recent attack. Exploring the ruins, they find a survivor, frightened and rambling. Roll on **NPC Encounter** (page [73](ch008.xhtml#local-npc-encounter-d10)) and **Cryptic Advice and Warnings** (page [71](ch008.xhtml#cryptic-advice-and-warnings-d10)). |
| 11 | 2 **Ashigaru** stand guard at an execution. The accused is buried up to their head below the high tide line. Amidst the gathered crowd, one voice cries out, insisting on the accused's innocence but the two guards are not moved. |
| 12 | D4 **Ashigaru** stand guard, blocking the path. |
| 13-14 | Along the swollen banks of the river, murky waters churn and froth with the relentless force of the deluge. If players wish to cross they must pass a DEX save. If they fail, a **Kappa** attacks with an **Enhanced** first attack. |
| 15 | The party sees two **Kappa** sitting on waterside rocks. |
| 16-17 | A **Suiko** leaps from the water, its teeth glistening as much as its scaled hide. |
| 18 | Tentacles surge forth, a **Koromodako** emerging from crashing waves. If the party is on land they can flee without having to make a DEX save. |
| 19 | A woman on the shore cries for help, cradling her baby. If the party investigates, they find it’s a **Nure onna** luring them into a trap. 1/3 chance that it’s quickly joined by an **Ushi-oni** emerging from the rocks. |
| 20 | A titanic figure rises, an impossibly dark **Umi-bozu** dark blocking the sky. |

### Forest Locations and Landmarks (D12)

| D12 | LOCATION OR LANDMARK |
|:---|:---|
| 1 | **Whispering Grove**: A dense thicket where the wind carries whispers, believed to be the voices of ancient spirits or forgotten ancestors. |
| 2 | **Ancient Tree**: A colossal tree, many centuries old, its bark inscribed with runes, said to be the resting place of a forest deity. |
| 3 | **Overgrown Ruins**: The remains of an ancient civilization, now covered in moss and vines, with strange carvings on the stone walls. |
| 4 | **Hunter’s Cabin**: A rustic cabin deep in the woods, often abandoned, though signs of recent use suggest otherwise. |
| 5 | **Wooden Watchtower**: A crumbling watchtower built by foresters or rangers, providing a vantage point over the sprawling forest. |
| 6 | **Spirit Hollow**: A dark, misty section of the forest where ghostly apparitions are said to appear during twilight. |
| 7 | **Abandoned Lumber Camp**: The remains of a once-thriving camp, now overtaken by nature, with rusted tools and overgrown buildings. |
| 8 | **Wolf Den**: A cave at the base of a large tree, home to a pack of wolves that have a mysterious connection to the forest spirits. |
| 9 | **Cursed Glade**: A clearing where the trees are twisted and blackened, and no birds sing. It is said that an evil force dwells here. |
| 10 | **Fallen Giant**: The massive trunk of a long-dead tree, hollowed out and used as shelter by travelers and forest creatures alike. |
| 11 | **Moss-Covered Shrine**: A small, forgotten shrine to a minor deity, covered in thick moss and vines, offering a sense of ancient protection. |
| 12 | **Bear Cave**: A large cave, home to a slumbering bear or something more dangerous, with the remains of past meals scattered about. |

### Forest Encounters (D12 or D20)

| D12/20 | ENCOUNTER |
|:---|:---|
| 1 | D6 **Wolves** stalk the party. |
| 2 | A colossal **Black Bear** towers over the party, fur bristling and eyes ablaze. |
| 3-4 | D6 **Bandits** shift among the foliage, waiting to ambush the party. |
| 5-6 | Visibility diminishes as a mist shrouds the surroundings in an eerie haze. If players wish to continue travel, they must WIL save, if they fail, they become lost and lose 2 Watch before the fog lifts. If they make camp for the day the fog lifts by morning. |
| 7 | The party stumbles upon the remains of a forest village, its charred remnants hinting at a recent attack. Exploring the ruins, they find a survivor, frightened and rambling. Roll on **NPC Encounter** (page [73](ch008.xhtml#local-npc-encounter-d10)) and **Cryptic Advice and Warnings** (page [71](ch008.xhtml#cryptic-advice-and-warnings-d10)). |
| 8 | A group of d4 **Ashigaru** is lost, led by a clueless **Samurai** who insists they know their way. |
| 9 | Beneath leaden skies, rain pelts relentlessly, soaking everything in its path. If players wish to continue travel, they must DEX save, if they fail, they lose 1 WIL. |
| 10-11 | Clad in rugged armor, a **Ronin** claiming to be a professional monster hunter emerges from the woods. |
| 12-13 | The party comes across a campfire smoldering with fading embers, casting a warm glow against the surrounding darkness. Nearby lies the charred remnants of a roasted rabbit. Yet, the campsite appears hastily abandoned. |
| 14-15 | Along the swollen banks of the river, murky waters churn and froth with the relentless force of the deluge. If players wish to cross they must pass a DEX save. If they fail, a **Kappa** attacks with an **Enhanced** first attack. |
| 16 | A sweet voice sounds from the nearby woods, calling to members of the party to come join them. If the party investigates, they find a **Jorogumo** waiting on its web. |
| 17 | Amidst dense foliage, a gnarled **Jubokko** looms, its branches creaking as they twist and move, threatening to ensnare anything that strays too close. |
| 18 | The party spots a **Nomori** uncoiling itself from around a bear as it begins to feast. |
| 19 | At first the party thinks they see a bear, but soon realize it’s an **Onikuma** rummaging through the guts of a horse to pick out meaty remains. |
| 20 | A giggle in the woods gets the party’s attention. The party’s light source goes out. If they do not have another, a **Nikusui** emerges and begins her hunt. |

### Hill Locations and Landmarks (D12)

| D12 | LOCATION OR LANDMARK |
|:---|:---|
| 1 | **Standing Stones**: A group of ancient, weathered stones atop a hill, etched with mysterious symbols from a forgotten age. |
| 2 | **Watchman’s Hill**: The highest hill in the region, crowned with an old watchtower, offering a clear view of the surrounding countryside. |
| 3 | **Burial Cairn**: A massive stone cairn marking the grave of a long-dead ruler or warrior, with rumors of treasure buried within. |
| 4 | **Windmill Ruins**: The crumbling remains of a once-functional windmill, now little more than a skeleton, its sails long gone. |
| 5 | **Echoing Hills**: A range of hills where sound carries strangely, making it difficult to determine the distance of noises. |
| 6 | **Hidden Valley**: A lush valley nestled between two hills, invisible from afar and home to rare plants and animals. |
| 7 | **Hilltop Battlefield**: The site of an ancient battle, with scattered bones and rusted weapons still embedded in the ground. |
| 8 | **Stone Fort Ruins**: The remains of a once-mighty hilltop fort, now reduced to crumbling walls and overgrown courtyards. |
| 9 | **Hilltop Shrine**: A small, sacred shrine dedicated. |
| 10 | **Wildflower Field**: A hill blanketed in colorful wildflowers, a beautiful and peaceful spot. |
| 11 | **Collapsed Mine**: An old, abandoned mine entrance carved into the side of a hill. |
| 12 | **Raven’s Perch**: A large, twisted tree atop a barren hill, always surrounded by a flock of ravens. |

### Hill Encounters (D12 or D20)

| D12/20 | ENCOUNTER |
|:---|:---|
| 1 | D6 **Wolves** stalk the party. |
| 2 | The party comes across 1-2 d4 **Wolves** 3-4 d4 **Vampire Bats** 5-6 a **Tiger** attacking an overturned carriage, trying to get to its occupants. |
| 3-4 | A **Giant Eagle** circles above, its keen eyes scanning the land below. It sees your party as a threat. |
| 5 | A **Mountain Lion** stalks silently, hungrily eyeing your party. |
| 6-8 | D6 **Bandits** shift among the foliage, waiting to ambush the party. |
| 9 | Beneath leaden skies, rain pelts relentlessly, soaking everything in its path. If players wish to continue travel, they must DEX save, if they fail, they lose 1 WIL. |
| 10 | A group of aristocrats on horseback gallop through the countryside, laughter mingling with the sound of hoofbeats. Players may listen in but may also be spotted. On a WIL save they overhear stories from the party - roll one **Rumor** (page [71](ch008.xhtml#rumors-d10)) and one **Local Event** (page [72](ch008.xhtml#local-events-d10)). |
| 11 | D6 **Ashigaru** are on a quest to retrieve their fallen comrade. |
| 12 | Two **Ashigaru** veterans drive a covered wagon with domesticated animals, seeking to settle and build a farm nearby. |
| 13-14 | The party stumbles upon a desolate village, its charred remnants hinting at a recent attack. Exploring the ruins, they find a survivor, frightened and rambling. Roll on **NPC Encounter** (page [73](ch008.xhtml#local-npc-encounter-d10)) and **Cryptic Advice and Warnings** (page [71](ch008.xhtml#cryptic-advice-and-warnings-d10)). |
| 15 | D4 **Ashigaru** stand guard, blocking the path. |
| 16 | A **Gashadokuro** rises from a desolate battlefield, empty sockets gleaming as it begins to hunt. |
| 17 | A woman on the shore cries for help, cradling her baby. If the party investigates, they find it’s a **Nure onna** luring them into a trap. |
| 18 | Small blue orbs of flickering flame dance, a swarm of d6 **Onibi** threatening to swarm the party. |
| 19 | In an eerie glow a **Reiki** stands in the distance, the ghost of a dead oni seeking an outlet for its fury. |
| 20 | A **Wanyudo** rolls toward the party, its infernal flames casting eerie shadows. |


### Mountain Locations and Landmarks (D12)

| D12 | LOCATION OR LANDMARK |
|:---|:---|
| 1 | **Frozen Waterfall**: A massive waterfall frozen in time, its surface slick and dangerous. |
| 2 | **Mountain Pass**: A treacherous, winding path through the mountains, often used by traders and adventurers seeking a shortcut. |
| 3 | **Mountain Hermit’s Hut**: A small, ramshackle hut belonging to a hermit who lives in solitude, offering cryptic advice to those who visit. |
| 4 | **Crystal Caverns**: A cave system filled with shimmering crystals. |
| 5 | **Abandoned Mine**: An old mining complex carved into the mountain, long abandoned. |
| 6 | **Giant’s Bridge**: A massive stone bridge spanning a deep chasm, supposedly built by giants in a bygone era. |
| 7 | **Mountain Lake**: A serene, crystal-clear lake high up in the mountains, fed by melting glaciers. |
| 8 | **Rockslide Ravine**: A dangerous ravine filled with unstable rocks and debris from frequent rockslides. |
| 9 | **Black Stone Crag**: A jagged, black rock formation jutting out from the mountain. |
| 10 | **Eagle’s Nest**: A large, flat-topped mountain where giant eagles are said to nest, protecting their territory fiercely. |
| 11 | **Mountain Tomb**: A hidden tomb carved into the mountainside, the resting place of a powerful ruler. |
| 12 | **Skyspire**: A sharp, narrow peak that reaches high into the clouds, nearly impossible to climb but said to offer a breathtaking view of the entire land. |


### Mountain Encounters (D12 or D20)

| D12/20 | ENCOUNTER |
|:---|:---|
| 1-2 | D6 **Wolves** stalk the party. |
| 3 | The party comes across 1-2 d4 **Wolves** 3-4 d4 **Vampire Bats** 5-6 a **Tiger** attacking an overturned carriage, trying to get to its occupants. |
| 4 | A **Giant Eagle** circles above, its keen eyes scanning the land below. It sees your party as a threat. |
| 5 | A **Mountain Lion** stalks silently, hungrily eyeing your party. |
| 6 | An ancient **Dire Wolf** prowls restlessly within a forgotten ravine, imprisoned by rocky confines. |
| 7 | The party stumbles upon a desolate village, its charred remnants hinting at a recent attack. Exploring the ruins, they find a survivor, frightened and rambling. Roll on **NPC Encounter** (page [73](ch008.xhtml#local-npc-encounter-d10)) and **Cryptic Advice and Warnings** (page [71](ch008.xhtml#cryptic-advice-and-warnings-d10)). |
| 8-9 | D6 **Bandits** shift among the foliage, waiting to ambush the party. |
| 10 | Beneath leaden skies, rain pelts relentlessly, soaking everything in its path. If players wish to continue travel, they must DEX save, if they fail, they lose 1 WIL. |
| 11 | A group of d4 **Ashigaru** is lost, led by a clueless **Samurai** who insists they know their way. |
| 12 | D4 **Ashigaru** stand guard, blocking the path. |
| 13-14 | On a jagged rock formation, three 1-2 **Kiju** 3-4 **Oni** 5-6 **Suiko** feast upon a torn-apart boar, savoring its blood as they wring out the lifeless corpse. |
| 15 | Amidst dense foliage, a gnarled **Jubokko** looms, its branches creaking as they twist and move, threatening to ensnare anything that strays too close. |
| 16 | The party spots a **Nomori** uncoiling itself from around a crushed bear as it begins to feast. |
| 17 | An **Oni** emerges with thunderous steps, an iron club in its hands. |
| 18 | At first the party thinks they see a bear, but soon realize it’s an **Onikuma** rummaging through the guts of a horse to pick out meaty remains. |
| 19 | A snowstorm suddenly descends on the party, the spectral figure of a **Yuki-Onna** drifting on the frail ahead. |
| 20 | An **Ushi-oni** emerges from its lair, skittering along spider-like legs, it’s ox head breathing toxic poison. |



### Plains Locations and Landmarks (D12)

| D12 | LOCATION OR LANDMARK |
|:---|:---|
| 1 | **Endless Grasslands**: A vast, flat expanse of tall grasses swaying in the wind, where the horizon seems to stretch forever. |
| 2 | **Stone Cairn Field**: A field dotted with ancient stone cairns, marking the graves of forgotten warriors or clans. |
| 3 | **Solitary Oak**: A massive, ancient oak tree standing alone in the plains, offering shade. |
| 4 | **Windmill Farm**: A collection of windmills scattered across the plains, used to grind grain or pump water from the ground. |
| 5 | **Herding Grounds**: An area where nomadic herders gather to care for their cattle or horses, a place of bustling activity and trade. |
| 6 | **Battlefield of the Fallen**: A blood-soaked plain where two great armies once clashed, now littered with rusting weapons and unmarked graves. |
| 7 | **Flowering Meadow**: A breathtaking stretch of land filled with vibrant wildflowers. |
| 8 | **Abandoned Farmstead**: The remains of a once-thriving farm, now reclaimed by the grasslands, with broken fences and collapsed buildings. |
| 9 | **Old Stone Road**: A cracked and overgrown ancient road, now rarely traveled. |
| 10 | **Wild Horse Range**: A wide, open area where wild horses roam free. |
| 11 | **Fallen Meteor Crater**: A large crater in the middle of the plains, the remnants of a fallen star. |
| 12 | **Plains Monolith**: A lone, towering stone slab standing in the middle of the plains, its purpose unknown. |



### Plains Encounters (D12 or D20)

| D12/20 | ENCOUNTER |
|:---|:---|
| 1 | A thunderous stampede of wild 1-2: D10 **Boar** 3-4: D10 **Deer** 4-6: D10 **Cattle** charges forth. |
| 2 | A sightless figure calls out to your party, shuffling along with a cane. He recounts tales of his past as a notorious bandit, revealing a darker truth—he never retired after losing his sight. He is a **Bandit Leader** and D6 **Bandits** step from hiding to join him. |
| 3 | D4 **Bandits** challenge the party. Amidst a bandit attack, a familiar face emerges among the robbers. |
| 4 | D6 **Bandits** shift among the foliage, waiting to ambush the party. |
| 5-6 | Beneath leaden skies, rain pelts relentlessly, soaking everything in its path. If players wish to continue travel, they must DEX save, if they fail, they lose 1 WIL. |
| 7 | The road turns muddy, soon two feet deep a tough to travel. Water in ditches bubbles, ominous signs of impending danger. If players wish to continue travel, they must DEX save, if they fail, they become bogged down and lose 1 Watch. |
| 8 | D10 **Ashigaru** are marching in disciplined formation, a patrol maintaining watch over the surrounding countryside, scanning the horizon for any sign of trouble amiss. |
| 9 | A group of samurai on horseback gallop through the countryside. Players may listen in to their conversation but may also be spotted. On a WIL save they overhear stories from the party – roll one **Rumor** (page [71](ch008.xhtml#rumors-d10)) and one **Local Event** (page [72](ch008.xhtml#local-events-d10)). |
| 10-11 | Weary refugees trudge along the dusty road, their faces etched with sorrow. The air bears the weight of their hardships as they seek solace in other lands. The refugees tell stories of their plight, roll on **Local** **Conflict or Dilemma** table (page [72](ch008.xhtml#conflict-or-dilemma-d10)). |
| 12 | A **Bandit** bound to a tree by a nearby village pleads for reprieve and forgiveness. |
| 13 | Two **Kijo** fight over the remains of a traveler. |
| 14-15 | A **Yurei** slowly appears. |
| 16 | An **Amanojaku's** whisper drifts across the wind, promises of untold riches or power, suspicion of other party members trying to sway characters into anger. |
| 17-18 | A **Gashadokuro** rises from a desolate battlefield, empty sockets gleaming as it begins to hunt. |
| 19 | A huge **Omukade** crawls from a crevice, impossibly fast, dangerously ferocious. |
| 20 | An **Oni** emerges with thunderous steps, an iron club in its hands. |



### Swamp Locations and Landmarks (D12)

| D12 | LOCATION OR LANDMARK |
|:---|:---|
| 1 | **Misty Bog**: A low-lying area covered in thick fog, where visibility is poor, and the ground squelches underfoot. |
| 2 | **Mangrove Forest**: A dense swamp of twisted mangrove trees, their roots creating natural bridges and hiding places beneath the water. |
| 3 | **Crocodile Lair**: A series of muddy caverns near the water's edge, home to massive, aggressive crocodiles. |
| 4 | **Ghost Marsh**: A hauntingly quiet part of the swamp where no animals seem to dwell. |
| 5 | **Firefly Glade**: A rare, dry patch of land within the swamp, illuminated by the constant glow of swarms of fireflies. |
| 6 | **Swamp Fortress**: A crumbling stone fortress built on a small island in the swamp, now abandoned and overrun with vines. |
| 7 | **Bloated Corpse Tree**: A grotesque tree growing in the middle of the swamp, with strange fruit that resemble swollen bodies hanging from its branches. |
| 8 | **Snake Den**: A patch of dense, tangled vines and roots. |
| 9 | **Blackwater Lake**: A deep, murky lake in the center of the swamp, where strange ripples disturb the surface. |
| 10 | **Sunken Village**: The remains of an old village, now mostly underwater, with rooftops barely visible above the murky swamp waters. |
| 11 | **Petrified Forest**: A section of the swamp where all the trees have turned to stone, their twisted shapes frozen in eerie poses. |
| 12 | **Abandoned Shrine**: A humble, overgrown shrine deep in the swamp. |



### Swamp Encounters (D12 or D20)

| D12/20 | ENCOUNTER |
|:---|:---|
| 1-2 | Visibility diminishes as a mist shrouds the surroundings in an eerie haze. If players wish to continue travel, they must WIL save, if they fail, they become lost and lose 2 Watch before the fog lifts. If they make camp for the day the fog lifts by morning. |
| 3 | Oh no, quicksand! Players must DEX save to avoid falling in. If they fail, they must STR save to remove themselves. If they fail 5 STR saves in a row, they die. Members of the party not trapped can help retrieve stuck players with a STR save. |
| 4-5 | As the party stops to consider an abandoned rowing boat bobs gently in the water, d4 **Kaizoku** jump out of the nearby foliage. |
| 6-7 | Beneath leaden skies, rain pelts relentlessly, soaking everything in its path. If players wish to continue travel, they must DEX save, if they fail, they lose 1 WIL. |
| 8 | The path turns muddy, soon two feet deep a tough to travel. Water in ditches bubbles, ominous signs of impending danger. If players wish to continue travel, they must DEX save, if they fail, they become bogged down and lose 1 Watch. |
| 9 | 2 **Ashigaru** stand guard at an execution. The accused is buried up to their head below the high tide line. Amidst the gathered crowd, one voice cries out, insisting on the accused's innocence but the two guards are not moved. |
| 10 | The party comes across a campfire smoldering with fading embers, casting a warm glow against the surrounding darkness. Nearby lies the charred remnants of a roasted rabbit. Yet, the campsite appears hastily abandoned. |
| 11-12 | D4 **Ashigaru** stand guard, blocking the path. |
| 13 | A giggle in the woods gets the party’s attention. The party’s light source goes out. If they do not have another, a **Nikusui** emerges and begins her hunt. |
| 14 | A sweet voice sounds from the nearby woods, calling to members of the party to come join them. If the party investigates, they find a **Jorogumo** waiting in its web. |
| 15-16 | A **Suiko** leaps from the water, its teeth glistening as much as its scaled hide. |
| 17 | The party spots a **Nomori** uncoiling itself from around a bear as it begins to feast. |
| 18 | A huge **Omukade** crawls from a crevice, impossibly fast, dangerously ferocious. |
| 19 | Small blue orbs of flickering flame dance, a swarm of d6 **Onibi** threatening to swarm the party. |
| 20 | An **Ushi-oni** emerges from its lair, skittering along spider-like legs, it’s ox head breathing toxic poison. |



### Urban Locations and Landmarks (D12)

| D12 | LOCATION OR LANDMARK |
|:---|:---|
| 1 | **Popular Teahouse**: A teahouse booming with business all hours of the day. |
| 2 | **Kabuki Theater**: A grand wooden theater where the performances are said to mirror true events happening elsewhere in the city. |
| 3 | **Riverside Market**: A bustling market alongside a slow-moving river, where merchants sell wares and hidden deals take place after dark. |
| 4 | **Cherry Blossom Park**: A park with endless rows of cherry blossom trees. |
| 5 | **Paper Lantern Street**: A winding street illuminated by countless paper lanterns. |
| 6 | **Imperial Pagoda**: A towering pagoda that offers a panoramic view of the city, once a retreat for emperors. |
| 7 | **Artisan Alley**: A narrow street filled with workshops, where blacksmiths, potters, and weavers craft their wares. |
| 8 | **Red Bridge**: An ornate bridge said to connect the world of the living with the world of spirits. |
| 9 | **Rice Warehouse District**: A series of massive wooden storehouses for rice, the lifeblood of the city, heavily guarded. |
| 10 | **Temple of Silent Prayer**: A serene temple where no one speaks, and pilgrims come to meditate in silence for days. |
| 11 | **Floating Dockyard**: A wooden dock that extends into the bay. |
| 12 | **Koi Pond Garden**: A peaceful garden with a pond full of koi. |



### Urban Encounters (D12 or D20)

| D12/20 | ENCOUNTER |
|:---|:---|
| 1 | A sightless figure calls out to your party, shuffling along with a cane. He recounts tales of his past as a notorious bandit, revealing a darker truth—he never retired after losing his sight. He is a **Bandit Leader** and D6 **Bandits** step from hiding to join him. |
| 2 | Beneath leaden skies, rain pelts relentlessly, soaking everything in its path. If players wish to continue travel, they must DEX save, if they fail, they lose 1 WIL. |
| 3 | D10 **Ashigaru** are marching in disciplined formation, a patrol maintaining watch over the surrounding countryside, scanning the horizon for any sign of trouble amiss. |
| 4 | A **Bandit** bound to a pole as punishment pleads for reprieve and forgiveness. |
| 5-6 | D6 **Ashigaru** emerge from a tavern, clearly drunk. One of their group spies your party and yells to you in a very unfriendly manner. |
| 7-8 | Amidst the vibrant marketplace, a **Ronin** shares stories with local villagers, tall tales of daring and monsters. |
| 9 | A local comes up to the party ranting and raving. Roll on **NPC Encounter** (page [73](ch008.xhtml#local-npc-encounter-d10)) and **Cryptic Advice and Warnings** (page [71](ch008.xhtml#cryptic-advice-and-warnings-d10)). |
| 10 | A friendly local invites your party to eat with their family. Roll on **NPC Encounter** (page [73](ch008.xhtml#local-npc-encounter-d10)). |
| 11 | Wary eyes follow the party, suspicion and mistrust thick in the air. Whispers ripple through the crowd, casting doubt upon the strangers. Players can not purchase any goods or services in this town. |
| 12-13 | 2 **Ashigaru** look from your party to a wanted poster and back again. Suspicion and uncertainty linger as wary gazes follow the party's every move. |
| 14 | Panic erupts in the streets as a frenzied mob of townsfolk flees through narrow alleyways, their terrified cries blending with the distant roar of an **Onryo**. |
| 15 | An **Amanojaku's** whisper drifts across the wind, promises of untold riches or power, suspicion of other party members trying to sway characters into anger. |
| 16-17 | A **Kuchisake-onna** glides forth, smiling, asking the party “Am I beautiful?” |
| 18 | A **Wanyudo** rolls toward the party, its infernal flames casting eerie shadows. |
| 19 | In an eerie glow a **Reiki** stands in the distance, the ghost of a dead oni seeking an outlet for its fury. |
| 20 | Your party stops and stares down an alleyway. You could have sworn you saw the floating head of a **Nukekubi**. |



### Settlement Size (D10)

**Towns** in feudal Japan often would not have permanent stores or shops, instead relying on local fairs held a few times a month. The development of castles and castle towns made permanent shops more common. What shops were available would still vary based on local conditions.

| D10 | SETTLEMENT SIZE                              |
|:----|:---------------------------------------------|
| 1-2 | Farm/Home (1-3 families)                     |
| 3-4 | Estate or Minor Post Station (50-100 people) |
| 5-6 | Town or Post Station (100-1000 people)       |
| 7-8 | Market Town (1000-5000 people)               |
| 9   | Castle Town (5000-10000 people)              |
| 10  | City (10000+ people)                         |


### Settlement Name Generator (3D20)

**Inspired by:** Richmond, Brian, “L5R Random Locale Generator,” The Goatman’s Goblet, May 15, 2018. https://www.goatmansgoblet.com/2018/05/l5r-random-locale-generator.html

| D20 | PART ONE    | PART TWO      | PART THREE |
|:----|:------------|:--------------|:-----------|
| 1   | Village of  | the Fallen    | River      |
| 2   | Port of     | the Dusty     | Forest     |
| 3   | Temple of   | the Bountiful | Wolf       |
| 4   | Castle of   | the Glorious  | Coin       |
| 5   | Town of     | the Celestial | Crane      |
| 6   | Fortress of | the Floral    | Tiger      |
| 7   | Inn off     | The Blessed   | Dragon     |
| 8   | Teahouse of | the Great     | Crab       |
| 9   | Shrine of   | the Lucky     | Cove       |
| 10  | Plains of   | the Ancient   | Moon       |
| 11  | Forest of   | the Lonely    | Turtle     |
| 12  | Mountain of | the Splendid  | Sun        |
| 13  | Island of   | the Pale      | Heavens    |
| 14  | Camp of     | the Blind     | Tides      |
| 15  | School of   | the Drunken   | Blade      |
| 16  | Halls of    | the Yellow    | Mirror     |
| 17  | Ruins of    | the Red       | Peaks      |
| 18  | Tower of    | the Imperial  | Dog        |
| 19  | Prison of   | the Exquisite | Leaf       |
| 20  | Library of  | the Broken    | Fortune    |



## The People and Their Stories

### Cryptic Advice and Warnings (D10)

| D10 | CRYPTIC ADVICE AND WARNINGS |
|:---|:---|
| **1** | “Beware the shadow that walks beside you, for its whispers lead to darkness.” |
| **2** | “The blossoms may bloom in peace, but the roots harbor secrets that stir with malice.” |
| **3** | “The river may seem tranquil but beware the serpent that lurks beneath the surface.” |
| **4** | “In the stillness of the night, spirits rise to haunt those who forget their sacrifice.” |
| **5** | “The path ahead may seem clear, but tread carefully, for even the most innocent step may awaken the wrath of gods long forgotten.” |
| **6** | “The winds of change blow strong, carrying whispers of a coming storm that will shake the foundations of the world.” |
| **7** | “The moon’s reflection may guide your way, but beware the shadows it casts, for they conceal the true nature of the world.” |
| **8** | “In the heart of the forest lies a darkness that hungers for the light of the living.” |
| **9** | “The stars above hold the answers, but the light reveals only what we are ready to face.” |
| **10** | “The past echoes in the present, and the future is written in the blood of those who dare to defy fate.” |


### Rumors (D10)

| D10 | RUMOR |
|:---|:---|
| 1 | A legendary samurai, long thought dead, has been sighted wandering the countryside, seeking revenge but no one knows what for. |
| 2 | The local lord’s heir has gone missing under mysterious circumstances, leading to whispers of foul play and treachery. |
| 3 | A hidden temple deep in the mountains holds the key to unlocking untold wealth and power for those brave enough to seek it out. |
| 4 | Strange lights have been seen dancing atop the nearby cliffs, believed to be the lanterns of vengeful spirits guiding lost souls to their doom. |
| 5 | The waters of the sacred river have turned blood-red, signaling an impending disaster foretold in ancient prophecy. |
| 6 | A famous entertainer has disappeared without a trace, leaving behind only rumors of her involvement with a shadowy underworld organization. |
| 7 | A mysterious illness has swept through the village, turning its victims into mindless zombies controlled by an unseen force. |
| 8 | A hidden clan of shinobi, rumored to possess supernatural abilities, lurks in the shadows, ready to strike at a moment’s notice. |
| 9 | A legendary beast, part dragon and part serpent, roams the mountains, terrorizing travelers, and demanding tribute from nearby villages. |
| 10 | The local magistrate is rumored to be in league with a group of bandits, lining his pockets with their ill-gotten gains. |



### Local Events (D10)

| D10 | EVENT |
|:---|:---|
| 1 | **Festival Celebration**: The village is bustling with activity as locals prepare for a traditional festival, featuring music, dance, and food. |
| 2 | **Market Day:** Merchants from neighboring villages gather in the town square to sell their goods, attracting crowds of buyers and traders. |
| 3 | **Village Meeting**: The elders convene to discuss important matters affecting the community, such as disputes, resource management, or defense strategies. |
| 4 | **Inspection**: A contingent of soldiers arrives in the village to assess its readiness for potential threats or conflicts, instilling both fear and respect among the residents. |
| 5 | **Bandit Raid**: The village is under attack by bandits, who seek to plunder its wealth and terrorize its inhabitants, prompting a desperate struggle for survival. |
| 6 | **Fire Outbreak**: A fire breaks out in the village, spreading rapidly and threatening to consume homes and livelihoods, requiring swift action to contain and extinguish. |
| 7 | **Illness Outbreak**: A mysterious illness sweeps through the village, causing widespread sickness and panic as villagers struggle to find a cure and stop spread. |
| 8 | **Animal Plague**: Livestock have been mysteriously dying without any symptoms. Locals fear sickness or more sinister elements at play. |
| 9 | **Ghostly Sightings**: Rumors spread of apparitions haunting the village, causing fear and superstition among the residents who seek explanations and protection. |
| 10 | **Planting**: Farmers labor in the fields, planting seedlings in preparation for the upcoming growing season, a crucial time for ensuring food security and prosperity. |



### Conflict or Dilemma (D10)

| D10 | CONFLICT OR DILEMMA |
|:---|:---|
| 1 | **Bandit Raids**: The area is plagued by frequent raids from bandits, who steal food, valuables, and terrorize the local population. |
| 2 | **Rivals**: Two powerful groups vie for control of the region, leading to escalating tensions and occasional skirmishes that threaten the peace. |
| 3 | **Drought and Famine**: A prolonged drought has dried up the fields and depleted food supplies, leading to widespread hunger and desperation among the villagers. |
| 4 | **Infestation**: Something in the nearby forests is preying on travelers and spreading fear. |
| 5 | **Land Dispute**: Disagreements over land ownership and boundaries have sparked conflicts between neighboring villages, with both sides refusing to back down. |
| 6 | **Cursed Shrine**: A sacred shrine in the area has been desecrated or cursed, causing misfortune and illness to befall anyone who visits or resides nearby. |
| 7 | **Samurai Discontent**: The samurai retainers serving the lord are dissatisfied, leading to murmurs of mutiny among the ranks. |
| 8 | **Tax Revolt**: The local magistrate has imposed heavy taxes on the villagers, squeezing them for every coin they have. The villagers organize a revolt, risking retaliation. |
| 9 | **Trade Blockade**: Bandits have blocked the area’s main routes, disrupting supplies. |
| 10 | **Unnatural Phenomenon**: Strange and inexplicable occurrences unsettle the village. |



### Local NPC Encounter (D10)

| D10 | ENCOUNTER |
|:---|:---|
| 1 | **Wandering Monk**: A humble monk travels the countryside, offering wisdom, guidance, and perhaps even mystical aid to those in need. |
| 2 | **Village Elder**: The wise elder of a nearby village seeks the party’s assistance in resolving a local conflict or dilemma. |
| 3 | **Ronin Seeking Employment**: A masterless samurai approaches the party, offering their sword in exchange for coin or a noble cause. |
| 4 | **Mysterious Stranger**: A cloaked figure with hidden motives approaches the party, offering cryptic advice or dire warnings of things to come. |
| 5 | **Local Farmer**: A humble farmer requests aid from the party in defending their land from bandits or supernatural threats. |
| 6 | **Entertainer**: A skilled entertainer from a nearby teahouse or pleasure district offers their services to the party, providing distraction and relaxation. |
| 7 | **Merchant or Trader**: A traveling merchant seeks to barter goods or valuable information with the party, offering rare commodities from distant lands. |
| 8 | **Spiritual Medium**: A practitioner of Shinto or Buddhist rituals offers to perform ceremonies or rituals for the party, providing blessings or exorcisms as needed. |
| 9 | **Local Craftsman**: A skilled artisan or craftsman offers to create or repair equipment for the party, showcasing their expertise in traditional crafts. |
| 10 | **Emissary of a Lord**: A representative of a local noble seeks the party’s aid in carrying out a mission or delivering a message of importance. |



### NPC Reactions (2D6)

| 2D6 | REACTION | 2D6  | REACTION |
|:----|:---------|:-----|:---------|
| 2   | Hostile  | 9-11 | Kind     |
| 3-5 | Wary     | 12   | Helpful  |
| 6-8 | Curious  |      |          |



### NPC Drive (D20)

| D20 | DRIVE | D20 | DRIVE |
|:---|:---|:---|:---|
| 1 | **Revenge** - Seeks vengeance for a past wrong | 11 | **Honor** - Lives by a strict code and seeks to maintain it |
| 2 | **Redemption** - Wants to atone for past mistakes | 12 | **Faith** - Devoted to their religion or a spiritual path |
| 3 | **Loyalty** - Devoted to a lord, family, or cause | 13 | **Fortune** - Driven by greed and a desire for wealth |
| 4 | **Survival** - Driven by the need to stay alive | 14 | **Healing** - Seeks to cure a loved one or themselves of an illness |
| 5 | **Knowledge** - Thirsts for forbidden lore or forgotten secrets | 15 | **Freedom** - Yearns to escape oppression or a difficult situation |
| 6 | **Power** - Ambitious and desires influence or authority | 16 | **Legacy** - Wishes to leave a lasting mark on the world |
| 7 | **Protection** - Wants to safeguard their loved ones or a community | 17 | **Balance** - Seeks to restore harmony or prevent chaos |
| 8 | **Peace** - Yearns for an end to conflict and suffering | 18 | **Vengeance/Nature** - Driven by a natural predator/prey instinct |
| 9 | **Justice** - Driven to uphold the law or right wrongs | 19 | **Curiosity** - Intrigued by the unknown and seeks answers |
| 10 | **Family** - Desires to reunite with or protect their family | 20 | **Pleasure** - Motivated by a desire for enjoyment and entertainment |



### NPC Combat Tactics (D20)

| D20 | COMBAT TACTIC | D20 | COMBAT TACTIC |
|:----|:--------------|:----|:--------------|
| 1   | Sneak         | 11  | Trap          |
| 2   | Conceal       | 12  | Retreat       |
| 3   | Grapple       | 13  | Evade         |
| 4   | Counter       | 14  | Entangle      |
| 5   | Counterfeit   | 15  | Demoralize    |
| 6   | Retreat       | 16  | Redirect      |
| 7   | Flank         | 17  | Redirect      |
| 8   | Stealth       | 18  | Feign         |
| 9   | Disguise      | 19  | Lure          |
| 10  | Parry         | 20  | Ambush        |



### NPC Quirks or Traits (D100)

| D100 | QUIRK OR TRAIT | D100 | QUIRK OR TRAIT |  | D100 | QUIRK OR TRAIT |
|:---|:---|:---|:---|----|:---|:---|
| 1 | Speaks through sign language | 34 | Has one or more gold teeth | **67** | Touches character during conversation |  |
| 2 | Uses foul language | 35 | Spits when talking | **68** | Animal bite/claw scar |  |
| 3 | Tattoo | 36 | Fidgets | **69** | Whispers |  |
| 4 | Hacking cough | 37 | Serious burn scar | **70** | Sniffs often |  |
| 5 | Has black eye | 38 | Calls by wrong names | **71** | Fascinated by fire |  |
| 6 | Giggles inappropriately | 39 | Always late | **72** | Scar |  |
| 7 | Clumsy | 40 | Tongue tied | **73** | Nods often |  |
| 8 | Picks nose | 41 | Greatly exaggerates | **74** | Very pale |  |
| 9 | Only eats meat | 42 | Mismatched eyes | **75** | Avoids crowds |  |
| 10 | Hands coins to beggar children | 43 | Writes down everything said | **76** | Thinks long before speaking |  |
| 11 | Blinks often | 44 | Talks loudly | **77** | Bruised extremities |  |
| 12 | Pathological liar | 45 | Limp | **78** | Claps hands often |  |
| 13 | Does not recognize personal space | 46 | Carries crumbs to feed birds | **79** | Closely examines everything |  |
| 14 | Hand covers mouth while speaking | 47 | Missing limb, joints, fingers, teeth | **80** | Never looks anyone in the eye |  |
| 15 | Is constantly cold/hot | 48 | Military Manner | **81** | Easily distracted |  |
| 16 | Conceited | 49 | Hard of hearing | **82** | Coughs regularly |  |
| 17 | Spotless, glossy boots | 50 | Always out of breath | **83** | Uses long words incorrectly |  |
| 18 | Survived torture, has no fingernails | 51 | Refers to self in third person | **84** | Sensitive to smells/light/noise |  |
| 19 | Mixes languages | 52 | Sweats profusely | **85** | Rubs back of neck |  |
| 20 | Ogles others openly | 53 | Long, lacquered nails | **86** | Flatulent |  |
| 21 | Hairless | 54 | Snorts while laughing | **87** | Rubs palms on thighs |  |
| 22 | Wears well-tended ancient weapon | 55 | Always repeats last spoken words | **88** | Clearly shows their emotions on their face |  |
| 23 | Crumbs in beard and clothes | 56 | Speaks to animals like people | **89** | Clears throat before speaking every time |  |
| 24 | Carries feed for birds | 57 | Whistles/hums frequently | **90** | Gestures wildly with hands |  |
| 25 | Phrases all sentences as questions | 58 | Gives a different name every meeting | **91** | Rope burns around neck or wrists |  |
| 26 | Holier than thou | 59 | Real/fake Accent | **92** | Gifts trinkets to guests |  |
| 27 | Keeps arms folded | 60 | Keeps hands in pockets | **93** | Is very literal |  |
| 28 | Rash | 61 | Underweight | **94** | Bandaged extremity |  |
| 29 | Taps foot incessantly | 62 | Hand on weapon | **95** | Speaks to themselves |  |
| 30 | Yawns often | 63 | Toothless | **96** | Squints |  |
| 31 | Wears obvious wig | 64 | Braggart | **97** | Uses bad jokes and puns |  |
| 32 | Asks rhetorical questions | 65 | Sucks on teeth | **98** | Wears clothes too big/small |  |
| 33 | Always eating or drinking | 66 | Takes everything personally | **99-00** | Roll again twice |  |



## Spark Tables



### Nouns (D100)

| D100 | NOUN      | D100 | NOUN         | D100 | NOUN        | D100 | NOUN         |
|:-----|:----------|:-----|:-------------|:-----|:------------|:-----|:-------------|
| 1    | Sword     | 26   | Saddle       | 51   | Ronin       | 76   | Fisherman    |
| 2    | Zen       | 27   | Kimono       | 52   | Shield      | 77   | Sash         |
| 3    | Gate      | 28   | Road         | 53   | Axe         | 78   | Bridge       |
| 4    | Geisha    | 29   | Fan          | 54   | Monastery   | 79   | Sliding Door |
| 5    | Spear     | 30   | Dragon       | 55   | Ink         | 80   | Dog          |
| 6    | Stall     | 31   | Stone        | 56   | Peasant     | 81   | Samurai      |
| 7    | Shrine    | 32   | Workshop     | 57   | Hot Spring  | 82   | Shogun       |
| 8    | Courtesan | 33   | Emperor      | 58   | Bamboo      | 83   | Port         |
| 9    | Flag      | 34   | Inn          | 59   | Tea         | 84   | Village      |
| 10   | Tatami    | 35   | Bonsai       | 60   | Servant     | 85   | Town         |
| 11   | Chair     | 36   | Valley       | 61   | Calligraphy | 86   | Garden       |
| 12   | Silk      | 37   | Palace       | 62   | Shop        | 87   | Wall         |
| 13   | Lake      | 38   | Family Crest | 63   | Dock        | 88   | Dojo         |
| 14   | Staff     | 39   | Forge        | 64   | Path        | 89   | City         |
| 15   | Katana    | 40   | Stables      | 65   | Waterfall   | 90   | Field        |
| 16   | Pond      | 41   | Warlord      | 66   | Window      | 91   | Forest       |
| 17   | Lantern   | 42   | Daimyo       | 67   | Marketplace | 92   | Temple       |
| 18   | Door      | 43   | Boat         | 68   | Rice        | 93   | Arrow        |
| 19   | Market    | 44   | Pottery      | 69   | Mountain    | 94   | Sake         |
| 20   | Bear      | 45   | Cat          | 70   | Manor       | 95   | Horse        |
| 21   | Armor     | 46   | Pagoda       | 71   | Banner      | 96   | Castle       |
| 22   | Table     | 47   | Theater      | 72   | Helmet      | 97   | Harbor       |
| 23   | Bowl      | 48   | Ninja        | 73   | Ship        | 98   | Roof         |
| 24   | River     | 49   | Robe         | 74   | Merchant    | 99   | Mask         |
| 25   | Scroll    | 50   | Bow          | 75   | Courtyard   | 00   | Brush        |



### Verbs (D100)

| D100 | VERB        | D100 | VERB        | D100 | VERB        | D100 | VERB       |
|:-----|:------------|:-----|:------------|:-----|:------------|:-----|:-----------|
| 1    | Strike      | 26   | Listen      | 51   | Find        | 76   | Outwit     |
| 2    | Defend      | 27   | Watch       | 52   | Uncover     | 77   | Outsmart   |
| 3    | Sneak       | 28   | Scout       | 53   | Investigate | 78   | Outflank   |
| 4    | Hide        | 29   | Investigate | 54   | Examine     | 79   | Outpace    |
| 5    | Observe     | 30   | Interrogate | 55   | Study       | 80   | Outrun     |
| 6    | Attack      | 31   | Negotiate   | 56   | Analyze     | 81   | Outman     |
| 7    | Deflect     | 32   | Persuade    | 57   | Solve       | 82   | Conspire   |
| 8    | Dodge       | 33   | Threaten    | 58   | Decode      | 83   | Scheme     |
| 9    | Parry       | 34   | Intimidate  | 59   | Track       | 84   | Plan       |
| 10   | Block       | 35   | Bargain     | 60   | Follow      | 85   | Plot       |
| 11   | Sprint      | 36   | Duel        | 61   | Pursue      | 86   | Manipulate |
| 12   | Climb       | 37   | Challenge   | 62   | Escape      | 87   | Deceive    |
| 13   | Crawl       | 38   | Defy        | 63   | Evade       | 88   | Trick      |
| 14   | Jump        | 39   | Resist      | 64   | Infiltrate  | 89   | Fool       |
| 15   | Run         | 40   | Submit      | 65   | Penetrate   | 90   | Mislead    |
| 16   | Walk        | 41   | Confront    | 66   | Sabotage    | 91   | Betray     |
| 17   | Stalk       | 42   | Conquer     | 67   | Inhibit     | 92   | Misdirect  |
| 18   | Ambush      | 43   | Surrender   | 68   | Disrupt     | 93   | Lure       |
| 19   | Assassinate | 44   | Raid        | 69   | Destroy     | 94   | Tempt      |
| 20   | Engage      | 45   | Plunder     | 70   | Assassinate | 95   | Seduce     |
| 21   | Retreat     | 46   | Pillage     | 71   | Defeat      | 96   | Distract   |
| 22   | Charge      | 47   | Ransack     | 72   | Overpower   | 97   | Divert     |
| 23   | Approach    | 48   | Explore     | 73   | Vanquish    | 98   | Beguile    |
| 24   | Flee        | 49   | Discover    | 74   | Crush       | 99   | Charm      |
| 25   | Lurk        | 50   | Search      | 75   | Outmaneuver | 00   | Enthrall   |



### Adjectives (D100)

| D100 | ADJECTIVE     | D100 | ADJECTIVE    | D100 | ADJECTIVE   | D100 | ADJECTIVE     |
|:-----|:--------------|:-----|:-------------|:-----|:------------|:-----|:--------------|
| 1    | Impervious    | 26   | Wise         | 51   | Dexterous   | 76   | Intrepid      |
| 2    | Inexorable    | 27   | Deadly       | 52   | Sharp-eared | 77   | Incisive      |
| 3    | Unyielding    | 28   | Perceptive   | 53   | Clever      | 78   | Unwavering    |
| 4    | Graceful      | 29   | Unshakeable  | 54   | Adaptable   | 79   | Daunting      |
| 5    | Relentless    | 30   | Tenacious    | 55   | Elusive     | 80   | Impressive    |
| 6    | Honorable     | 31   | Brave        | 56   | Inscrutable | 81   | Courageous    |
| 7    | Fearless      | 32   | Cunning      | 57   | Determined  | 82   | Vigilant      |
| 8    | Sharp         | 33   | Confident    | 58   | Astute      | 83   | Shrewd        |
| 9    | Unbending     | 34   | Agile        | 59   | Mysterious  | 84   | Daring        |
| 10   | Compromising  | 35   | Stealthy     | 60   | Patient     | 85   | Unrelenting   |
| 11   | Impenetrable  | 36   | Strong       | 61   | Elegant     | 86   | Evasive       |
| 12   | Loyal         | 37   | Agile-minded | 62   | Acute       | 87   | Indomitable   |
| 13   | Insidious     | 38   | Diligent     | 63   | Disciplined | 88   | Charismatic   |
| 14   | Unshakable    | 39   | Quick        | 64   | Ruthless    | 89   | Calculating   |
| 15   | Intense       | 40   | Resourceful  | 65   | Formidable  | 90   | Deceptive     |
| 16   | Unwavering    | 41   | Unyielding   | 66   | Observant   | 91   | Unbreakable   |
| 17   | Unassailable  | 42   | Silent       | 67   | Unflinching | 92   | Noble         |
| 18   | Astute        | 43   | Unbending    | 68   | Unshakeable | 93   | Cautious      |
| 19   | Shadowy       | 44   | Sharp-eyed   | 69   | Agile       | 94   | Indefatigable |
| 20   | Skilled       | 45   | Prudent      | 70   | Formidable  | 95   | Wily          |
| 21   | Unfaltering   | 46   | Resilient    | 71   | Versatile   | 96   | Inflexible    |
| 22   | Unpredictable | 47   | Steadfast    | 72   | Formidable  | 97   | Flexible      |
| 23   | Fierce        | 48   | Decisive     | 73   | Small       | 98   | Sagacious     |
| 24   | Swift         | 49   | Dauntless    | 74   | Stalwart    | 99   | Unyielding    |
| 25   | Unflinching   | 50   | Agile        | 75   | Enigmatic   | 00   | Charming      |

