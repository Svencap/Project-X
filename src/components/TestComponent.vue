<template>
  <v-container>
    <v-card class="pa-6">
      <!-- Cover Section -->
      <v-card class="mb-6 pa-6 text-center cover-card">
        <h1 class="text-h3 mb-4">Добро пожаловать на наш сайт!</h1>
        <p class="text-h6 mb-4">
          Здесь вы найдете разнообразные лексические упражнения, <br>
          специально разработанные для учащихся 10&nbsp;класса. 
        </p>
        <v-row justify="center">
          <v-col cols="12" md="8">
            <v-card outlined class="pa-4">
              <p class="text-body-1 mb-2">
                Мы предлагаем интерактивные задания, которые помогут вам: 
              </p>
              <div class="text-center">
                <span>Углубить знание словарного запаса <br></span>
                <span>Подготовиться к экзаменам и контрольным работам</span>
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-card>

      <h1 class="text-h4 mb-6">Module 1 «Strong ties»</h1>
      
      <!-- Exercise 1 - Word Accent -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 1. Choose the correct accent of the words:</h2>
        
        <div v-for="(word, index) in accentWords" :key="index" class="mb-4">
          <h3 class="subtitle-1 mb-2">{{ word.word }}</h3>
          <v-radio-group v-model="answers.ex1[index]">
            <v-radio v-for="(option, optIndex) in word.options" 
                     :key="optIndex" 
                     :label="option" 
                     :value="option"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise(1)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex1 !== null" :type="results.ex1 ? 'success' : 'error'" class="mt-2">
          {{ results.ex1 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 2 - Pronunciation -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 2. Choose the correct pronunciation of the words:</h2>
        
        <div v-for="(word, index) in pronunciationWords" :key="index" class="mb-4">
          <h3 class="subtitle-1 mb-2">{{ word.word }}</h3>
          <v-radio-group v-model="answers.ex2[index]">
            <v-radio v-for="(option, optIndex) in word.options" 
                     :key="optIndex" 
                     :label="option" 
                     :value="option"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise(2)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex2 !== null" :type="results.ex2 ? 'success' : 'error'" class="mt-2">
          {{ results.ex2 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 3 - Synonyms -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 3. Find a synonym for the words:</h2>
        
        <div v-for="(word, index) in synonymWords" :key="index" class="mb-4">
          <h3 class="subtitle-1 mb-2">{{ word.word }}</h3>
          <v-radio-group v-model="answers.ex3[index]">
            <v-radio v-for="(option, optIndex) in word.options" 
                     :key="optIndex" 
                     :label="option" 
                     :value="option"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise(3)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex3 !== null" :type="results.ex3 ? 'success' : 'error'" class="mt-2">
          {{ results.ex3 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 4 - Extra Word -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 4. Choose an extra word in each column:</h2>
        
        <div v-for="(group, index) in extraWordGroups" :key="index" class="mb-4">
          <h3 class="subtitle-1 mb-2">Group {{ index + 1 }}</h3>
          <v-radio-group v-model="answers.ex4[index]">
            <v-radio v-for="(word, wordIndex) in group" 
                     :key="wordIndex" 
                     :label="word" 
                     :value="word"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise(4)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex4 !== null" :type="results.ex4 ? 'success' : 'error'" class="mt-2">
          {{ results.ex4 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 5 - Negative Adjectives -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 5. Choose all the adjectives that have a negative meaning:</h2>
        <v-checkbox v-model="answers.ex5" label="Jealous" value="Jealous"></v-checkbox>
        <v-checkbox v-model="answers.ex5" label="Mean" value="Mean"></v-checkbox>
        <v-checkbox v-model="answers.ex5" label="Trusting" value="Trusting"></v-checkbox>
        <v-checkbox v-model="answers.ex5" label="Moody" value="Moody"></v-checkbox>
        <v-checkbox v-model="answers.ex5" label="Caring" value="Caring"></v-checkbox>
        <v-btn color="primary" @click="checkExercise(5)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex5 !== null" :type="results.ex5 ? 'success' : 'error'" class="mt-2">
          {{ results.ex5 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 6 - Synonyms -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 6. Choose synonyms for the word "look after":</h2>
        <v-checkbox v-model="answers.ex6" label="Take care" value="Take care"></v-checkbox>
        <v-checkbox v-model="answers.ex6" label="Be careful" value="Be careful"></v-checkbox>
        <v-checkbox v-model="answers.ex6" label="Watch" value="Watch"></v-checkbox>
        <v-checkbox v-model="answers.ex6" label="Hope" value="Hope"></v-checkbox>
        <v-checkbox v-model="answers.ex6" label="Expect" value="Expect"></v-checkbox>
        <v-btn color="primary" @click="checkExercise(6)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex6 !== null" :type="results.ex6 ? 'success' : 'error'" class="mt-2">
          {{ results.ex6 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 7 - Parts of Speech -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 7. Identify which parts of speech these words are:</h2>
        
        <div v-for="(word, index) in partsOfSpeech" :key="index" class="mb-4">
          <h3 class="subtitle-1 mb-2">{{ word.word }}</h3>
          <v-radio-group v-model="answers.ex7[index]">
            <v-radio v-for="(option, optIndex) in word.options" 
                     :key="optIndex" 
                     :label="option" 
                     :value="option"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise(7)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex7 !== null" :type="results.ex7 ? 'success' : 'error'" class="mt-2">
          {{ results.ex7 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 8 - Idioms -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 8. Connect the words so that you get an idiom:</h2>
        
        <div v-for="(idiom, idiomKey) in idiomExercises" :key="idiomKey" class="mb-8">
          <h3 class="subtitle-1 mb-2">{{ idiomKey.toUpperCase() }}) {{idiom.description}}</h3>
          <div class="d-flex flex-wrap mb-2">
            <v-chip 
              v-for="(word, wordIndex) in idiom.words" 
              :key="`${idiomKey}-${wordIndex}`"
              class="ma-1 draggable-chip"
              draggable
              @dragstart="startDrag($event, word, idiomKey)"
              @dragend="dragEnd"
            >
              {{ word }}
            </v-chip>
          </div>
          <div 
            class="drop-zone"
            @drop="onDrop($event, idiomKey)"
            @dragover.prevent
            @dragenter.prevent
          >
            <div v-if="!answers[`ex8${idiomKey}`]" class="placeholder-text">
              Drop words here to form the idiom
            </div>
            <div v-else class="idiom-text">
              {{ answers[`ex8${idiomKey}`] }}
            </div>
          </div>
          <v-btn 
            small 
            @click="clearAnswer(`ex8${idiomKey}`)" 
            class="mt-2 clear-btn"
            :disabled="!answers[`ex8${idiomKey}`]"
          >
            Clear
          </v-btn>
        </div>
        <v-btn color="primary" @click="checkExercise(8)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex8 !== null" :type="results.ex8 ? 'success' : 'error'" class="mt-2">
          {{ results.ex8 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 9 - Word Associations -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 9. Match as many adjectives and verbs as possible to one noun "designer"</h2>
        <v-checkbox v-model="answers.ex9" label="Create" value="Create"></v-checkbox>
        <v-checkbox v-model="answers.ex9" label="Artistic" value="Artistic"></v-checkbox>
        <v-checkbox v-model="answers.ex9" label="Take care" value="Take care"></v-checkbox>
        <v-checkbox v-model="answers.ex9" label="Moody" value="Moody"></v-checkbox>
        <v-checkbox v-model="answers.ex9" label="Stylish" value="Stylish"></v-checkbox>
        <v-btn color="primary" @click="checkExercise(9)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex9 !== null" :type="results.ex9 ? 'success' : 'error'" class="mt-2">
          {{ results.ex9 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 10 - Phrase Completion -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 10. Choose one of the two words to get a phrase:</h2>
        
        <div class="mb-4">
          <h3 class="subtitle-1 mb-2">Fashion ___</h3>
          <v-radio-group v-model="answers.ex10_1">
            <v-radio label="Trendy" value="Trendy"></v-radio>
            <v-radio label="Well-dressed" value="Well-dressed"></v-radio>
          </v-radio-group>
        </div>

        <div class="mb-4">
          <h3 class="subtitle-1 mb-2">Eyes ___</h3>
          <v-radio-group v-model="answers.ex10_2">
            <v-radio label="comical" value="comical"></v-radio>
            <v-radio label="sharp" value="sharp"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise(10)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex10 !== null" :type="results.ex10 ? 'success' : 'error'" class="mt-2">
          {{ results.ex10 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 11 - Fill in the Gaps -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 11. Fill in the gaps in the text:</h2>
        <p class="mb-4">
          In our busy lives, it's important to take time for ourselves and the
          people we care about. I have a group of 1……
          <v-select v-model="answers.ex11_1" :items="options.ex11_1" class="d-inline-block" style="width: 150px;"></v-select>
          who I love to 2…... 
          <v-select v-model="answers.ex11_2" :items="options.ex11_2" class="d-inline-block" style="width: 150px;"></v-select>
          We often spend our weekends together, 3…..
          <v-select v-model="answers.ex11_3" :items="options.ex11_3" class="d-inline-block" style="width: 150px;"></v-select>
          or 4…... 
          <v-select v-model="answers.ex11_4" :items="options.ex11_4" class="d-inline-block" style="width: 150px;"></v-select>
          Each of us is unique—some are 5…..
          <v-select v-model="answers.ex11_5" :items="options.ex11_5" class="d-inline-block" style="width: 150px;"></v-select>
          in a playful way, while others are 6…..
          <v-select v-model="answers.ex11_6" :items="options.ex11_6" class="d-inline-block" style="width: 150px;"></v-select>
          and 7…... 
          <v-select v-model="answers.ex11_7" :items="options.ex11_7" class="d-inline-block" style="width: 150px;"></v-select>
          It's this diversity that makes our time together so special.
          Whether we're discussing our favorite songs or sharing ideas for
          new projects, I always look forward to our next get-together!
        </p>
        <v-btn color="primary" @click="checkExercise(11)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex11 !== null" :type="results.ex11 ? 'success' : 'error'" class="mt-2">
          {{ results.ex11 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Exercise 12 - Questions -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 12. Put questions to the highlighted words:</h2>
        
        <div class="mb-4">
          <p class="mb-2"><strong>Her outfit was incredibly trendy</strong>, making her the center of attention at the party.</p>
          <v-checkbox v-model="answers.ex12_1" label="What was her outfit like?" value="What was her outfit like?"></v-checkbox>
          <v-checkbox v-model="answers.ex12_1" label="Whose outfit was trendy?" value="Whose outfit was trendy?"></v-checkbox>
          <v-checkbox v-model="answers.ex12_1" label="What made her the center of attention at the party?" value="What made her the center of attention at the party?"></v-checkbox>
        </div>
        
        <div class="mb-4">
          <p class="mb-2"><strong>The movie was surprisingly comical</strong>, providing a much-needed laugh after a long week.</p>
          <v-checkbox v-model="answers.ex12_2" label="Was the movie comical?" value="Was the movie comical?"></v-checkbox>
          <v-checkbox v-model="answers.ex12_2" label="Why did the movie make you laugh?" value="Why did the movie make you laugh?"></v-checkbox>
          <v-checkbox v-model="answers.ex12_2" label="What was the movie?" value="What was the movie?"></v-checkbox>
        </div>
        
        <v-btn color="primary" @click="checkExercise(12)" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex12 !== null" :type="results.ex12 ? 'success' : 'error'" class="mt-2">
          {{ results.ex12 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Test Section -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Test</h2>
        
        <!-- Test Question 1 -->
        <div class="mb-6">
          <h3 class="subtitle-1 mb-2">1. Fill in the gaps in the sentences using the appropriate words from the list:</h3>
          
          <div class="mb-2">
            <p>She is very <v-select v-model="answers.test1_1" :items="options.test1" class="d-inline-block" style="width: 200px;"></v-select> and always helps others in need.</p>
          </div>
          
          <div class="mb-2">
            <p>His <v-select v-model="answers.test1_2" :items="options.test1" class="d-inline-block" style="width: 200px;"></v-select> nature makes him popular among friends.</p>
          </div>
          
          <div class="mb-2">
            <p>Many people admire her <v-select v-model="answers.test1_3" :items="options.test1" class="d-inline-block" style="width: 200px;"></v-select> style.</p>
          </div>
          
          <div class="mb-2">
            <p>He is really <v-select v-model="answers.test1_4" :items="options.test1" class="d-inline-block" style="width: 200px;"></v-select> in sports and loves to compete.</p>
          </div>
          
          <div class="mb-2">
            <p>You can see that she is <v-select v-model="answers.test1_5" :items="options.test1" class="d-inline-block" style="width: 200px;"></v-select> about her abilities.</p>
          </div>
        </div>
        
        <!-- Test Question 2 -->
        <div class="mb-6">
          <h3 class="subtitle-1 mb-2">2. Choose definitions for the following words:</h3>
          
          <div v-for="(word, index) in testDefinitions" :key="index" class="mb-4">
            <h4 class="body-1 mb-2">{{ word.word }}</h4>
            <v-radio-group v-model="answers[`test2_${index+1}`]">
              <v-radio v-for="(option, optIndex) in word.options" 
                       :key="optIndex" 
                       :label="option" 
                       :value="option"></v-radio>
            </v-radio-group>
          </div>
        </div>
        
        <!-- Test Question 3 -->
        <div class="mb-6">
          <h3 class="subtitle-1 mb-2">3. Choose the right continuation of the sentence:</h3>
          
          <div v-for="(question, index) in testContinuations" :key="index" class="mb-4">
            <p class="mb-2">{{ question.question }}</p>
            <v-radio-group v-model="answers[`test3_${index+1}`]">
              <v-radio v-for="(option, optIndex) in question.options" 
                       :key="optIndex" 
                       :label="option" 
                       :value="option"></v-radio>
            </v-radio-group>
          </div>
        </div>
        
        <v-btn color="primary" @click="checkTest" class="mt-2">Check Test</v-btn>
        <v-alert v-if="testResult !== null" :type="testResult ? 'success' : 'error'" class="mt-2">
          {{ testResult ? 'Test passed successfully!' : 'Test failed. Please try again.' }}
        </v-alert>
      </v-card>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      answers: {
        // Exercise 1
        ex1: [],
        // Exercise 2
        ex2: [],
        // Exercise 3
        ex3: [],
        // Exercise 4
        ex4: [],
        // Exercise 5
        ex5: [],
        // Exercise 6
        ex6: [],
        // Exercise 7
        ex7: [],
        // Exercise 8
        ex8a: '',
        ex8b: '',
        ex8c: '',
        ex8d: '',
        ex8e: '',
        // Exercise 9
        ex9: [],
        // Exercise 10
        ex10_1: null,
        ex10_2: null,
        // Exercise 11
        ex11_1: null,
        ex11_2: null,
        ex11_3: null,
        ex11_4: null,
        ex11_5: null,
        ex11_6: null,
        ex11_7: null,
        // Exercise 12
        ex12_1: [],
        ex12_2: [],
        // Test answers
        test1_1: null,
        test1_2: null,
        test1_3: null,
        test1_4: null,
        test1_5: null,
        test2_1: null,
        test2_2: null,
        test2_3: null,
        test2_4: null,
        test2_5: null,
        test3_1: null,
        test3_2: null,
        test3_3: null,
        test3_4: null,
        test3_5: null,
        test3_6: null,
        test3_7: null
      },
      accentWords: [
        { word: "Appearance", options: ["Ooo", "oOo", "ooO"] },
        { word: "Qualities", options: ["Ooo", "oOo", "ooO"] },
        { word: "Personality", options: ["oooOo", "Ooooo", "ooOoo", "ooooO"] },
        { word: "Activities", options: ["Oooo", "oOoo", "ooOo", "oooO"] },
        { word: "Voluntary", options: ["Oooo", "oOoo", "ooOo", "oooO"] },
        { word: "Aggressive", options: ["Ooo", "oOo", "ooO"] },
        { word: "Dedicated", options: ["Oooo", "oOoo", "ooOo", "oooO"] }
      ],
      pronunciationWords: [
        { word: "patient", options: ["[ˈpeɪʃnt]", "[peɪnt]", "[paɪnt]"] },
        { word: "Jealous", options: ["[ˈʤeləs]", "[ˈʤeləus]", "[ˈʤɪləs]"] },
        { word: "Dishonest", options: ["[dɪsˈɒnəst]", "[dɪsˈɒnɪst]", "[dɪzˈɒnɪst]"] },
        { word: "Supportive", options: ["[səˈpɔːtɪv]", "[səˈpɔrːtɪv]", "[saˈpɔːtɪv]"] },
        { word: "Personality", options: ["[pɜːsəˈnalɪtɪ]", "[pɜːsəˈnælɪtɪ]", "[pɜːsɒˈnælɪtɪ]"] },
        { word: "Countless", options: ["[ˈkɒʊntlɪs]", "[ˈkaʊntlæs]", "[ˈkaʊntlɪs]"] },
        { word: "Comfortable", options: ["[ˈkʌmf(ə)təb(ə)l]", "[ˈkamf(ə)təb(ə)l]", "[ˈkəmf(ə)təb(ə)l]"] }
      ],
      synonymWords: [
        { word: "trusting", options: ["Calm", "Honest", "Admired"] },
        { word: "Aggressive", options: ["Violent", "Moody", "Dishonest"] },
        { word: "Well-meaning", options: ["Beautiful", "Loyal", "Caring"] },
        { word: "Personality", options: ["Quality", "Fashion", "Identity"] },
        { word: "Plump", options: ["Thick", "Wonderful", "Jealous"] },
        { word: "Decisive", options: ["Aggressive", "Mean", "Crucial"] },
        { word: "Slender", options: ["Trusting", "Thin", "Plump"] }
      ],
      extraWordGroups: [
        ["Supporting", "Caring", "Jealous", "Creative", "Well-meaning"],
        ["Tall", "Short", "Kind", "Slim"],
        ["Friendly", "Generous", "Blue", "Honest"],
        ["Curly", "Straight", "Beautiful", "Fast"],
        ["Patient", "Rude", "Cheerful", "Long"],
        ["Strong", "Weak", "Intelligent", "Tall"]
      ],
      partsOfSpeech: [
        { word: "Well-dressed", options: ["Verb", "Adjective", "Adverb"] },
        { word: "Designer", options: ["Verb", "Adjective", "Noun"] },
        { word: "Hang out", options: ["Verb", "Adjective", "Adverb"] },
        { word: "Chat online", options: ["Verb", "Adjective", "Adverb"] },
        { word: "Thoughtful", options: ["Verb", "Adjective", "Adverb"] },
        { word: "Message", options: ["Verb", "Noun", "Adverb"] },
        { word: "Voluntary", options: ["Verb", "Adjective", "Adverb"] }
      ],
      idiomExercises: {
        a: {
          description: "A bear with a sore head",
          words: ["a", "bear", "with", "a", "sore", "head"]
        },
        b: {
          description: "Give the cold shoulder",
          words: ["the", "cold", "give", "shoulder"]
        },
        c: {
          description: "Be a pain in the neck",
          words: ["a", "pain", "in", "be", "the", "neck"]
        },
        d: {
          description: "Get off my back",
          words: ["off", "my", "back", "get"]
        },
        e: {
          description: "Get on nerves",
          words: ["on", "get", "nerves"]
        }
      },
      options: {
        ex11_1: ['Respected', 'slender', 'bloomed'],
        ex11_2: ['Go on trip', 'hang out with', 'do sport'],
        ex11_3: ['Chat online', 'send text', 'do voluntary work'],
        ex11_4: ['Listen to music', 'play games', 'send emails'],
        ex11_5: ['aggressive', 'mean', 'disonest'],
        ex11_6: ['Thoughtful', 'well-meaning', 'decisive'],
        ex11_7: ['Brightened', 'Creative', 'trendy'],
        test1: ['charming', 'athletic', 'unique', 'confident', 'kindhearted']
      },
      testDefinitions: [
        { 
          word: "Friendly",
          options: [
            "being kind and pleasant to others.",
            "someone who prefers to be alone and avoid social interactions.",
            "characterized by a supportive and welcoming attitude."
          ]
        },
        { 
          word: "Confident",
          options: [
            "having a strong belief in oneself and one's abilities.",
            "feeling uncertain and insecure about decisions.",
            "displaying self-assurance and poise in social situations."
          ]
        },
        { 
          word: "Unique",
          options: [
            "being the only one of its kind, unlike anything else.",
            "commonly found or widely replicated.",
            "possessing distinct characteristics that set it apart from others."
          ]
        },
        { 
          word: "Charming",
          options: [
            "delightful and pleasing in a way that attracts others.",
            "boring and uninteresting in personality or appearance.",
            "having a special quality that makes someone endearing or appealing."
          ]
        },
        { 
          word: "Athletic",
          options: [
            "physically fit and skilled in sports or physical activities.",
            "lifestyle.",
            "characterized by agility, stamina, and coordination in physical pursuits."
          ]
        }
      ],
      testContinuations: [
        {
          question: "She has beautiful long hair, which makes her...",
          options: [
            "look very impressive.",
            "always wear a hat.",
            "prefer to stay inside."
          ]
        },
        {
          question: "He is very charming and friendly, so people often...",
          options: [
            "want to get to know him better.",
            "ignore his presence.",
            "find him annoying."
          ]
        },
        {
          question: "They have a lot of confidence, which helps them...",
          options: [
            "achieve their goals.",
            "avoid challenges.",
            "be afraid of new experiences."
          ]
        },
        {
          question: "She is very tall and athletic, so she...",
          options: [
            "dislikes sports.",
            "excels in physical activities.",
            "prefers to stay indoors."
          ]
        },
        {
          question: "He is known for his kind heart, which means he often...",
          options: [
            "volunteers in the community.",
            "keeps to himself.",
            "never helps others."
          ]
        },
        {
          question: "Her sense of style is unique, making her...",
          options: [
            "blend in with the crowd.",
            "stand out in any event.",
            "always wear the same clothes."
          ]
        },
        {
          question: "He has a great sense of humor, so he...",
          options: [
            "makes everyone laugh.",
            "rarely smiles.",
            "avoids social situations."
          ]
        }
      ],
      correctAnswers: {
        // Exercise 1
        ex1: ["oOo", "Ooo", "ooOoo", "Oooo", "oOoo", "oOo", "oOoo"],
        // Exercise 2
        ex2: ["[ˈpeɪʃnt]", "[ˈʤeləs]", "[dɪsˈɒnɪst]", "[səˈpɔːtɪv]", "[pɜːsəˈnælɪtɪ]", "[ˈkaʊntlɪs]", "[ˈkʌmf(ə)təb(ə)l]"],
        // Exercise 3
        ex3: ["Honest", "Violent", "Caring", "Identity", "Thick", "Crucial", "Thin"],
        // Exercise 4
        ex4: ["Jealous", "Kind", "Blue", "Fast", "Long", "Intelligent"],
        // Exercise 5
        ex5: ["Jealous", "Mean", "Moody"],
        // Exercise 6
        ex6: ["Take care", "Watch"],
        // Exercise 7
        ex7: ["Adjective", "Noun", "Verb", "Verb", "Adjective", "Noun", "Adjective"],
        // Exercise 8
        ex8a: "a bear with a sore head",
        ex8b: "give the cold shoulder",
        ex8c: "be a pain in the neck",
        ex8d: "get off my back",
        ex8e: "get on nerves",
        // Exercise 9
        ex9: ["Create", "Artistic", "Stylish"],
        // Exercise 10
        ex10_1: "Trendy",
        ex10_2: "sharp",
        // Exercise 11
        ex11_1: "Respected",
        ex11_2: "hang out with",
        ex11_3: "Chat online",
        ex11_4: "play games",
        ex11_5: "aggressive",
        ex11_6: "well-meaning",
        ex11_7: "Creative",
        // Exercise 12
        ex12_1: ["What was her outfit like?"],
        ex12_2: ["What was the movie?"],
        // Test answers
        test1_1: "kindhearted",
        test1_2: "charming",
        test1_3: "unique",
        test1_4: "athletic",
        test1_5: "confident",
        test2_1: "being kind and pleasant to others.",
        test2_2: "having a strong belief in oneself and one's abilities.",
        test2_3: "being the only one of its kind, unlike anything else.",
        test2_4: "delightful and pleasing in a way that attracts others.",
        test2_5: "physically fit and skilled in sports or physical activities.",
        test3_1: "look very impressive.",
        test3_2: "want to get to know him better.",
        test3_3: "achieve their goals.",
        test3_4: "excels in physical activities.",
        test3_5: "volunteers in the community.",
        test3_6: "stand out in any event.",
        test3_7: "makes everyone laugh."
      },
      results: {
        ex1: null,
        ex2: null,
        ex3: null,
        ex4: null,
        ex5: null,
        ex6: null,
        ex7: null,
        ex8: null,
        ex9: null,
        ex10: null,
        ex11: null,
        ex12: null
      },
      testResult: null,
      draggedWord: null,
      draggedIdiomKey: null
    }
  },
  methods: {
    startDrag(event, word, idiomKey) {
      this.draggedWord = word;
      this.draggedIdiomKey = idiomKey;
      event.dataTransfer.setData('text/plain', word);
      event.dataTransfer.effectAllowed = 'move';
    },
    
    dragEnd() {
      this.draggedWord = null;
      this.draggedIdiomKey = null;
    },
    
    onDrop(event, targetIdiomKey) {
      event.preventDefault();
      if (this.draggedIdiomKey === targetIdiomKey) {
        const currentAnswer = this.answers[`ex6${targetIdiomKey}`];
        if (!currentAnswer || currentAnswer !== this.draggedWord) {
          this.answers[`ex6${targetIdiomKey}`] = currentAnswer 
            ? `${currentAnswer} ${this.draggedWord}` 
            : this.draggedWord;
        }
      }
    },
    
    clearAnswer(field) {
      this.answers[field] = '';
    },
    
    checkExercise(exerciseNumber) {
    switch(exerciseNumber) {
      case 1:
        this.results.ex1 = JSON.stringify(this.answers.ex1) === 
                          JSON.stringify(this.correctAnswers.ex1);
        break;
      case 2:
        this.results.ex2 = JSON.stringify(this.answers.ex2) === 
                          JSON.stringify(this.correctAnswers.ex2);
        break;
      case 3:
        this.results.ex3 = JSON.stringify(this.answers.ex3) === 
                          JSON.stringify(this.correctAnswers.ex3);
        break;
      case 4:
        this.results.ex4 = JSON.stringify(this.answers.ex4) === 
                          JSON.stringify(this.correctAnswers.ex4);
        break;
      case 5:
        this.results.ex5 = JSON.stringify([...this.answers.ex5].sort()) === 
                          JSON.stringify([...this.correctAnswers.ex5].sort());
        break;
      case 6:
        this.results.ex6 = JSON.stringify([...this.answers.ex6].sort()) === 
                          JSON.stringify([...this.correctAnswers.ex6].sort());
        break;
      case 7:
        this.results.ex7 = JSON.stringify(this.answers.ex7) === 
                          JSON.stringify(this.correctAnswers.ex7);
        break;
      case 8:
        this.results.ex8 = (
          this.answers.ex8a.toLowerCase().replace(/\s+/g, ' ') === this.correctAnswers.ex8a.toLowerCase() &&
          this.answers.ex8b.toLowerCase().replace(/\s+/g, ' ') === this.correctAnswers.ex8b.toLowerCase() &&
          this.answers.ex8c.toLowerCase().replace(/\s+/g, ' ') === this.correctAnswers.ex8c.toLowerCase() &&
          this.answers.ex8d.toLowerCase().replace(/\s+/g, ' ') === this.correctAnswers.ex8d.toLowerCase() &&
          this.answers.ex8e.toLowerCase().replace(/\s+/g, ' ') === this.correctAnswers.ex8e.toLowerCase()
        );
        break;
      case 9:
        this.results.ex9 = JSON.stringify([...this.answers.ex9].sort()) === 
                          JSON.stringify([...this.correctAnswers.ex9].sort());
        break;
      case 10:
        this.results.ex10 = (
          this.answers.ex10_1 === this.correctAnswers.ex10_1 &&
          this.answers.ex10_2 === this.correctAnswers.ex10_2
        );
        break;
      case 11:
        this.results.ex11 = (
          this.answers.ex11_1 === this.correctAnswers.ex11_1 &&
          this.answers.ex11_2 === this.correctAnswers.ex11_2 &&
          this.answers.ex11_3 === this.correctAnswers.ex11_3 &&
          this.answers.ex11_4 === this.correctAnswers.ex11_4 &&
          this.answers.ex11_5 === this.correctAnswers.ex11_5 &&
          this.answers.ex11_6 === this.correctAnswers.ex11_6 &&
          this.answers.ex11_7 === this.correctAnswers.ex11_7
        );
        break;
      case 12:
        this.results.ex12 = (
          JSON.stringify([...this.answers.ex12_1].sort()) === JSON.stringify([...this.correctAnswers.ex12_1].sort()) &&
          JSON.stringify([...this.answers.ex12_2].sort()) === JSON.stringify([...this.correctAnswers.ex12_2].sort())
        );
        break;
    }
  },

  checkTest() {
    const testCorrect = (
      this.answers.test1_1 === this.correctAnswers.test1_1 &&
      this.answers.test1_2 === this.correctAnswers.test1_2 &&
      this.answers.test1_3 === this.correctAnswers.test1_3 &&
      this.answers.test1_4 === this.correctAnswers.test1_4 &&
      this.answers.test1_5 === this.correctAnswers.test1_5 &&
      this.answers.test2_1 === this.correctAnswers.test2_1 &&
      this.answers.test2_2 === this.correctAnswers.test2_2 &&
      this.answers.test2_3 === this.correctAnswers.test2_3 &&
      this.answers.test2_4 === this.correctAnswers.test2_4 &&
      this.answers.test2_5 === this.correctAnswers.test2_5 &&
      this.answers.test3_1 === this.correctAnswers.test3_1 &&
      this.answers.test3_2 === this.correctAnswers.test3_2 &&
      this.answers.test3_3 === this.correctAnswers.test3_3 &&
      this.answers.test3_4 === this.correctAnswers.test3_4 &&
      this.answers.test3_5 === this.correctAnswers.test3_5 &&
      this.answers.test3_6 === this.correctAnswers.test3_6 &&
      this.answers.test3_7 === this.correctAnswers.test3_7
    );
    
    this.testResult = testCorrect;
  },
  }
}
</script>

<style scoped>
.drop-zone {
  min-height: 50px;
  border: 2px dashed #ccc;
  padding: 10px;
  margin-bottom: 10px;
}

.placeholder-text {
  color: #999;
  font-style: italic;
}

.idiom-text {
  font-weight: bold;
}

.clear-btn {
  margin-right: 10px;
}
</style>