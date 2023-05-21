# Program to Identify Verbs and Provide Synonyms using Natural Language Processing

## Aim
Construct a Python program to read a text from a file. Identify the verbs from the text file and provide synonyms for all verbs using Natural Language Processing.

## Algorithm
1. Import the necessary libraries: `nltk` and `wordnet`.
2. Define a function `get_verbs(sentence)` to identify verbs in a given sentence using part-of-speech tagging.
3. Define a function `get_synonyms(word)` to get synonyms for a given word using the WordNet corpus.
4. Define a function `read_text_file(file_path)` to read text from a file and return the content as a string.
5. In the main program:
   - Set the `file_path` variable to the path of the input text file.
   - Read the text from the file using the `read_text_file()` function.
   - Tokenize the text into sentences using the `sent_tokenize()` function from the `nltk` library.
   - Initialize an empty list `all_verbs` to store all identified verbs.
   - Initialize an empty dictionary `synonyms_dict` to store the synonyms for each verb.
   - Iterate over each sentence:
     - Call the `get_verbs()` function to identify verbs in the sentence.
     - Append the identified verbs to the `all_verbs` list.
     - For each verb, call the `get_synonyms()` function to get its synonyms and store them in the `synonyms_dict` dictionary.
   - Print the verbs and their synonyms.
6. Execute the main program.

## Program
```python
import nltk
from nltk.corpus import wordnet

nltk.download('averaged_perceptron_tagger')
nltk.download('wordnet')
nltk.download('punkt')

# Function to identify verbs in a sentence
def get_verbs(sentence):
    verbs = []
    pos_tags = nltk.pos_tag(nltk.word_tokenize(sentence))
    for word, tag in pos_tags:
        if tag.startswith('V'):  # Verbs start with 'V' in the POS tag
            verbs.append(word)
    return verbs


def get_synonyms(word):
    synonyms = []
    for syn in wordnet.synsets(word):
        for lemma in syn.lemmas():
            synonyms.append(lemma.name())
    return synonyms


def read_text_file(file_path):
    with open(file_path, 'r') as file:
        text = file.read()
    return text


def main():
    file_path = 'sample.txt'  # Replace with your text file path

    text = read_text_file(file_path)
    sentences = nltk.sent_tokenize(text)

    all_verbs = []
    synonyms_dict = {}

    for sentence in sentences:
        verbs = get_verbs(sentence)
        all_verbs.extend(verbs)
        for verb in verbs:
            synonyms = get_synonyms(verb)
            synonyms_dict[verb] = synonyms

    with open('output.csv', 'w', newline='') as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(['Verb', 'Synonyms'])
        for verb, synonyms in synonyms_dict.items():
            writer.writerow([verb, ', '.join(synonyms)])


if __name__ == '__main__':
    main()
```
## Output
|Verb|Synonyms|
|---|---|
|was|Washington, Evergreen\_State, WA, be, be, be, exist, be, be, equal, be, constitute, represent, make\_up, comprise, be, be, follow, embody, be, personify, be, be, live, be, cost, be|
|named|name, call, name, identify, name, nominate, make, appoint, name, nominate, constitute, name, mention, advert, bring\_up, cite, name, refer, identify, discover, key, key\_out, distinguish, describe, name, list, name, diagnose, name|
|lived|populate, dwell, live, inhabit, live, survive, last, live, live\_on, go, endure, hold\_up, hold\_out, exist, survive, live, subsist, be, live, know, experience, live, live|
|loved|love, love, enjoy, love, sleep\_together, roll\_in\_the\_hay, love, make\_out, make\_love, sleep\_with, get\_laid, have\_sex, know, do\_it, be\_intimate, have\_intercourse, have\_it\_away, have\_it\_off, screw, fuck, jazz, eff, hump, lie\_with, bed, have\_a\_go\_at\_it, bang, get\_it\_on, bonk, loved|
|explore|research, search, explore, explore, explore, explore|
|exploring|research, search, explore, explore, explore, explore|
|came|come, come\_up, arrive, get, come, come, come, come, follow, come, issue\_forth, come, hail, come, come, come, come, fall, come, come, total, number, add\_up, come, amount, come, add\_up, amount, come, come\_in, occur, come, derive, come, descend, do, fare, make\_out, come, get\_along, come, come|
|peered|peer|
|see|see, see, understand, realize, realise, see, witness, find, see, visualize, visualise, envision, project, fancy, see, figure, picture, image, see, consider, reckon, view, regard, learn, hear, get\_word, get\_wind, pick\_up, find\_out, get\_a\_line, discover, see, watch, view, see, catch, take\_in, meet, run\_into, encounter, run\_across, come\_across, see, determine, check, find\_out, see, ascertain, watch, learn, see, check, insure, see\_to\_it, ensure, control, ascertain, assure, see, see, visit, see, attend, take\_care, look, see, see, go\_steady, go\_out, date, see, see, see, see, examine, see, experience, see, go\_through, see, escort, see, interpret, construe, see|
|decided|decide, make\_up\_one's\_mind, determine, decide, settle, resolve, adjudicate, decide, decide, distinct, decided|
|climb|ascent, acclivity, rise, raise, climb, upgrade, climb, climbing, mounting, climb, mount, climb, climb\_up, mount, go\_up, climb, wax, mount, climb, rise, climb, climb, rise, go\_up, climb|
|led|light-emitting\_diode, LED, lead, take, direct, conduct, guide, leave, result, lead, lead, lead, head, lead, run, go, pass, lead, extend, head, lead, lead, top, contribute, lead, conduce, conduct, lead, direct, go, lead, precede, lead, run, lead, moderate, chair, lead|
|fell|hide, fell, fell, felled\_seam, fell, fell, drop, strike\_down, cut\_down, fly, fell, vanish, fell, fall, descend, fall, go\_down, come\_down, fall, fall, come, precipitate, come\_down, fall, fall, fall, fall, shine, strike, fall, fall, decrease, diminish, lessen, fall, fall, fall, fall, fall, fall, fall, fall, accrue, fall, fall, light, fall, return, pass, devolve, fall, fall, fall\_down, fall, hang, fall, flow, fall, fall, fall, fall, fall, fall, fall, descend, settle, barbarous, brutal, cruel, fell, roughshod, savage, vicious|
|landed|land, set\_down, land, put\_down, bring\_down, bring, land, land, land, land, set\_ashore, shore, down, shoot\_down, land, landed|
|found|found, establish, set\_up, found, launch, establish, found, plant, constitute, institute, establish, base, ground, found, find, happen, chance, bump, encounter, detect, observe, find, discover, notice, find, regain, determine, find, find\_out, ascertain, find, feel, witness, find, see, line\_up, get\_hold, come\_up, find, discover, find, discover, find, find, rule, find, receive, get, find, obtain, incur, find, recover, retrieve, find, regain, find, find\_oneself, find, found|
|were|be, be, be, exist, be, be, equal, be, constitute, represent, make\_up, comprise, be, be, follow, embody, be, personify, be, be, live, be, cost, be|
|talking|talk, talking, talk, speak, talk, speak, utter, mouth, verbalize, verbalise, speak, talk, spill, talk, spill\_the\_beans, let\_the\_cat\_out\_of\_the\_bag, talk, tattle, blab, peach, babble, sing, babble\_out, blab\_out, lecture, talk|
|had|have, have\_got, hold, have, feature, experience, receive, have, get, own, have, possess, get, let, have, consume, ingest, take\_in, take, have, have, hold, throw, have, make, give, have, have, have, experience, have, induce, stimulate, cause, have, get, make, accept, take, have, receive, have, suffer, sustain, have, get, have, get, make, give\_birth, deliver, bear, birth, have, take, have|
|learned|learn, larn, acquire, learn, hear, get\_word, get\_wind, pick\_up, find\_out, get\_a\_line, discover, see, memorize, memorise, con, learn, learn, study, read, take, teach, learn, instruct, determine, check, find\_out, see, ascertain, watch, learn, erudite, learned, knowing, knowledgeable, learned, lettered, well-educated, well-read, conditioned, learned|
|arguing|controversy, contention, contestation, disputation, disceptation, tilt, argument, arguing, argue, reason, argue, contend, debate, fence, argue, indicate|
|do|bash, do, brawl, do, doh, ut, Doctor\_of\_Osteopathy, DO, make, do, perform, execute, do, do, perform, do, fare, make\_out, come, get\_along, cause, do, make, practice, practise, exercise, do, suffice, do, answer, serve, do, make, act, behave, do, serve, do, do, manage, dress, arrange, set, do, coif, coiffe, coiffure, do|
|terrorizing|terrorize, terrorise, terrify, terrorize, terrorise|
|help|aid, assist, assistance, help, assistant, helper, help, supporter, aid, assistance, help, avail, help, service, help, assist, aid, help, aid, help, facilitate, help\_oneself, help, serve, help, help, avail, help, help|
|defeat|defeat, licking, frustration, defeat, get\_the\_better\_of, overcome, defeat, kill, shoot\_down, defeat, vote\_down, vote\_out|
|went|travel, go, move, locomote, go, proceed, move, go, go\_away, depart, become, go, get, go, run, go, run, go, pass, lead, extend, proceed, go, go, go, sound, go, function, work, operate, go, run, run\_low, run\_short, go, move, go, run, survive, last, live, live\_on, go, endure, hold\_up, hold\_out, go, die, decease, perish, go, exit, pass\_away, expire, pass, kick\_the\_bucket, cash\_in\_one's\_chips, buy\_the\_farm, conk, give-up\_the\_ghost, drop\_dead, pop\_off, choke, croak, snuff\_it, belong, go, go, start, go, get\_going, move, go, go, go, blend, go, blend\_in, go, lead, fit, go, rifle, go, go, plump, go, fail, go\_bad, give\_way, die, give\_out, conk\_out, go, break, break\_down|
|challenged|challenge, dispute, gainsay, challenge, challenge, challenge, take\_exception|
|surprised|surprise, surprise, storm, surprise, surprised|
|agreed|agree, hold, concur, concord, agree, match, fit, correspond, check, jibe, gibe, tally, agree, harmonize, harmonise, consort, accord, concord, fit\_in, agree, agree, agree, agree, agreed, in\_agreement|
|fight|battle, conflict, fight, engagement, fight, fighting, combat, scrap, competitiveness, fight, fight, fight, contend, fight, struggle, fight, oppose, fight\_back, fight\_down, defend, fight, struggle, crusade, fight, press, campaign, push, agitate|
|fought|contend, fight, struggle, fight, oppose, fight\_back, fight\_down, defend, fight, struggle, crusade, fight, press, campaign, push, agitate|
|defeated|defeated, discomfited, get\_the\_better\_of, overcome, defeat, kill, shoot\_down, defeat, vote\_down, vote\_out, defeated, defeated, disappointed, discomfited, foiled, frustrated, thwarted|
|saving|economy, saving, rescue, deliverance, delivery, saving, preservation, saving, salvage, salve, relieve, save, save, preserve, save, carry\_through, pull\_through, bring\_through, save, save, lay\_aside, save\_up, save, make\_unnecessary, deliver, redeem, save, spare, save, save, economize, economise, keep\_open, hold\_open, keep, save, write, save, redemptive, redeeming, saving, saving|
|threw|throw, throw, shed, cast, cast\_off, shake\_off, throw, throw\_off, throw\_away, drop, throw, thrust, give, throw, throw, flip, switch, project, cast, contrive, throw, throw, bewilder, bemuse, discombobulate, throw, hurl, throw, hold, throw, have, make, give, throw, throw, throw, confuse, throw, fox, befuddle, fuddle, bedevil, confound, discombobulate|
|return|tax\_return, income\_tax\_return, return, return, homecoming, return, coming\_back, restitution, return, restoration, regaining, return, return, issue, take, takings, proceeds, yield, payoff, recurrence, return, rejoinder, retort, return, riposte, replication, comeback, counter, return\_key, return, return, paying\_back, getting\_even, return, return, reappearance, return, return, render, return, revert, return, retrovert, regress, turn\_back, hark\_back, return, come\_back, recall, return, take\_back, bring\_back, return, return, retort, come\_back, repay, return, riposte, rejoin, come\_back, return, refund, return, repay, give\_back, render, deliver, return, reelect, return, fall, return, pass, devolve, return, render, yield, return, give, generate, return|
|said|state, say, tell, allege, aver, say, suppose, say, read, say, order, tell, enjoin, say, pronounce, articulate, enounce, sound\_out, enunciate, say, say, say, say, say, say, aforesaid, aforementioned, said|
|climbed|climb, climb\_up, mount, go\_up, climb, wax, mount, climb, rise, climb, climb, rise, go\_up, climb|
|reached|reach, make, attain, hit, arrive\_at, gain, reach, hit, attain, reach, reach\_out, reach, get\_through, get\_hold\_of, contact, achieve, accomplish, attain, reach, reach, extend\_to, touch, reach, make, get\_to, progress\_to, pass, hand, reach, pass\_on, turn\_over, give, strive, reach, strain|
|glad|gladiolus, gladiola, glad, sword\_lily, glad, glad, happy, glad, beaming, glad|
|be|beryllium, Be, glucinium, atomic\_number\_4, be, be, be, exist, be, be, equal, be, constitute, represent, make\_up, comprise, be, be, follow, embody, be, personify, be, be, live, be, cost, be|
|knew|know, cognize, cognise, know, know, know, know, experience, live, acknowledge, recognize, recognise, know, know, sleep\_together, roll\_in\_the\_hay, love, make\_out, make\_love, sleep\_with, get\_laid, have\_sex, know, do\_it, be\_intimate, have\_intercourse, have\_it\_away, have\_it\_off, screw, fuck, jazz, eff, hump, lie\_with, bed, have\_a\_go\_at\_it, bang, get\_it\_on, bonk, know, know, know|
|forget|forget, bury, forget, block, blank\_out, draw\_a\_blank, forget, forget, leave|
|are|are, ar, be, be, be, exist, be, be, equal, be, constitute, represent, make\_up, comprise, be, be, follow, embody, be, personify, be, be, live, be, cost, be|
|used|use, utilize, utilise, apply, employ, use, habituate, use, expend, use, practice, apply, use, use, used, exploited, ill-used, put-upon, used, victimized, victimised, secondhand, used|
|explored|research, search, explore, explore, explore, explore|
|tell|Tell, William\_Tell, state, say, tell, tell, tell, narrate, recount, recite, order, tell, enjoin, say, tell, assure, tell, tell, evidence, distinguish, separate, differentiate, secern, secernate, severalize, severalise, tell, tell\_apart|
|create|make, create, create, create, create, create, make, produce, make, create|
|show|show, display, show, show, appearance, show, show, demo, exhibit, present, demonstrate, prove, demonstrate, establish, show, shew, testify, bear\_witness, prove, evidence, show, show, picture, depict, render, show, express, show, evince, indicate, point, designate, show, show, show\_up, read, register, show, record, show, usher, show, show|
## Result
Hence, we have successfully implemented a program for Natural Language Processing.
