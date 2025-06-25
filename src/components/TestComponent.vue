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
        <h2 class="text-h6 mb-4">Exercise 1. Match the word with the correct word stress pattern. "O" are stressed syllables, "o" are unstressed.</h2>
        
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

      <!-- NEW Exercise 8 - Definitions -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 8. Choose the right definition.</h2>
        
        <div v-for="(item, index) in definitionExercises" :key="index" class="mb-4">
          <h3 class="subtitle-1 mb-2">{{ item.word }}</h3>
          <v-radio-group v-model="answers.ex8[index]">
            <v-radio v-for="(option, optIndex) in item.options" 
                     :key="optIndex" 
                     :label="option" 
                     :value="optIndex"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise('ex8')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex8 !== null" :type="results.ex8 ? 'success' : 'error'" class="mt-2">
          {{ results.ex8 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>

      <!-- NEW Exercise 9 - Word Associations -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 9. Give the word you associate with:</h2>
        
        <div v-for="(item, index) in wordAssociation" :key="index" class="mb-4">
          <h3 class="subtitle-1 mb-2">Word: {{ item.word }}</h3>
          <v-radio-group v-model="answers.ex9[index]">
            <v-radio v-for="(option, optIndex) in item.options" 
                     :key="optIndex" 
                     :label="option" 
                     :value="optIndex"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise('ex9')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex9 !== null" :type="results.ex9 ? 'success' : 'error'" class="mt-2">
          {{ results.ex9 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>

      <!-- NEW Exercise 10 - General Meaning -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 10. Choose the word with the general meaning:</h2>
        
        <div v-for="(item, index) in generalMeaning" :key="index" class="mb-4">
          <v-radio-group v-model="answers.ex10[index]">
            <v-radio v-for="(option, optIndex) in item.options" 
                     :key="optIndex" 
                     :label="option" 
                     :value="optIndex"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise('ex10')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex10 !== null" :type="results.ex10 ? 'success' : 'error'" class="mt-2">
          {{ results.ex10 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>

      <!-- OLD Exercise 8 (now 11) - Idioms -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 11. Connect the words so that you get an idiom:</h2>
        
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
            <div v-if="!answers.ex11[idiomKey]" class="placeholder-text">
              Drop words here to form the idiom
            </div>
            <div v-else class="idiom-text">
              {{ answers.ex11[idiomKey] }}
            </div>
          </div>
          <v-btn 
            small 
            @click="clearAnswer('ex11', idiomKey)" 
            class="mt-2 clear-btn"
            :disabled="!answers.ex11[idiomKey]"
          >
            Clear
          </v-btn>
        </div>
        <v-btn color="primary" @click="checkExercise('ex11')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex11 !== null" :type="results.ex11 ? 'success' : 'error'" class="mt-2">
          {{ results.ex11 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>

      <!-- OLD Exercise 9 (now 12) - Word Associations -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 12. Match as many adjectives and verbs as possible to one noun "designer"</h2>
        <v-checkbox v-model="answers.ex12" label="Create" value="Create"></v-checkbox>
        <v-checkbox v-model="answers.ex12" label="Artistic" value="Artistic"></v-checkbox>
        <v-checkbox v-model="answers.ex12" label="Take care" value="Take care"></v-checkbox>
        <v-checkbox v-model="answers.ex12" label="Moody" value="Moody"></v-checkbox>
        <v-checkbox v-model="answers.ex12" label="Stylish" value="Stylish"></v-checkbox>
        <v-btn color="primary" @click="checkExercise('ex12')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex12 !== null" :type="results.ex12 ? 'success' : 'error'" class="mt-2">
          {{ results.ex12 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- OLD Exercise 10 (now 13) - Phrase Completion -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 13. Choose one of the two words to get a phrase:</h2>
        
        <div class="mb-4">
          <h3 class="subtitle-1 mb-2">Fashion ___</h3>
          <v-radio-group v-model="answers.ex13_1">
            <v-radio label="Trendy" value="Trendy"></v-radio>
            <v-radio label="Well-dressed" value="Well-dressed"></v-radio>
          </v-radio-group>
        </div>

        <div class="mb-4">
          <h3 class="subtitle-1 mb-2">Eyes ___</h3>
          <v-radio-group v-model="answers.ex13_2">
            <v-radio label="comical" value="comical"></v-radio>
            <v-radio label="sharp" value="sharp"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise('ex13')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex13 !== null" :type="results.ex13 ? 'success' : 'error'" class="mt-2">
          {{ results.ex13 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>

      <!-- NEW Exercise 14 - Translation -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 14. Find the correct translation of phrases:</h2>
        
        <div v-for="(item, index) in translationExercises" :key="index" class="mb-4">
          <h3 class="subtitle-1 mb-2">{{ item.phrase }}</h3>
          <v-radio-group v-model="answers.ex14[index]">
            <v-radio v-for="(option, optIndex) in item.options" 
                     :key="optIndex" 
                     :label="option" 
                     :value="optIndex"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise('ex14')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex14 !== null" :type="results.ex14 ? 'success' : 'error'" class="mt-2">
          {{ results.ex14 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>

      <!-- OLD Exercise 11 (now 15) - Fill in the Gaps -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 15. Fill in the gaps in the text:</h2>
        <p class="mb-4">
          In our busy lives, it's important to take time for ourselves and the
          people we care about. I have a group of 1……
          <v-select v-model="answers.ex15_1" :items="options.ex15_1" class="d-inline-block" style="width: 150px;"></v-select>
          who I love to 2…... 
          <v-select v-model="answers.ex15_2" :items="options.ex15_2" class="d-inline-block" style="width: 150px;"></v-select>
          We often spend our weekends together, 3…..
          <v-select v-model="answers.ex15_3" :items="options.ex15_3" class="d-inline-block" style="width: 150px;"></v-select>
          or 4…... 
          <v-select v-model="answers.ex15_4" :items="options.ex15_4" class="d-inline-block" style="width: 150px;"></v-select>
          Each of us is unique—some are 5…..
          <v-select v-model="answers.ex15_5" :items="options.ex15_5" class="d-inline-block" style="width: 150px;"></v-select>
          in a playful way, while others are 6…..
          <v-select v-model="answers.ex15_6" :items="options.ex15_6" class="d-inline-block" style="width: 150px;"></v-select>
          and 7…... 
          <v-select v-model="answers.ex15_7" :items="options.ex15_7" class="d-inline-block" style="width: 150px;"></v-select>
          It's this diversity that makes our time together so special.
          Whether we're discussing our favorite songs or sharing ideas for
          new projects, I always look forward to our next get-together!
        </p>
        <v-btn color="primary" @click="checkExercise('ex15')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex15 !== null" :type="results.ex15 ? 'success' : 'error'" class="mt-2">
          {{ results.ex15 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- OLD Exercise 12 (now 16) - Questions -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 16. Put questions to the highlighted words:</h2>
        
        <div class="mb-4">
          <p class="mb-2"><strong>Her outfit was incredibly trendy</strong>, making her the center of attention at the party.</p>
          <v-checkbox v-model="answers.ex16_1" label="What was her outfit like?" value="What was her outfit like?"></v-checkbox>
          <v-checkbox v-model="answers.ex16_1" label="Whose outfit was trendy?" value="Whose outfit was trendy?"></v-checkbox>
          <v-checkbox v-model="answers.ex16_1" label="What made her the center of attention at the party?" value="What made her the center of attention at the party?"></v-checkbox>
        </div>
        
        <div class="mb-4">
          <p class="mb-2"><strong>The movie was surprisingly comical</strong>, providing a much-needed laugh after a long week.</p>
          <v-checkbox v-model="answers.ex16_2" label="Was the movie comical?" value="Was the movie comical?"></v-checkbox>
          <v-checkbox v-model="answers.ex16_2" label="Why did the movie make you laugh?" value="Why did the movie make you laugh?"></v-checkbox>
          <v-checkbox v-model="answers.ex16_2" label="What was the movie?" value="What was the movie?"></v-checkbox>
        </div>
        
        <v-btn color="primary" @click="checkExercise('ex16')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex16 !== null" :type="results.ex16 ? 'success' : 'error'" class="mt-2">
          {{ results.ex16 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>

      <!-- NEW Exercise 17 - Quiz -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 17. Answer the questions:</h2>
        
        <div v-for="(item, index) in quizQuestions" :key="index" class="mb-4">
          <h3 class="subtitle-1 mb-2">{{ item.question }}</h3>
          <v-radio-group v-model="answers.ex17[index]">
            <v-radio v-for="(option, optIndex) in item.options" 
                     :key="optIndex" 
                     :label="option" 
                     :value="optIndex"></v-radio>
          </v-radio-group>
        </div>
        
        <v-btn color="primary" @click="checkExercise('ex17')" class="mt-2">Check</v-btn>
        <v-alert v-if="results.ex17 !== null" :type="results.ex17 ? 'success' : 'error'" class="mt-2">
          {{ results.ex17 ? 'Correct!' : 'Incorrect!' }}
        </v-alert>
      </v-card>
      
      <!-- Test Section (now Exercise 18) -->
      <v-card outlined class="mb-6 pa-4">
        <h2 class="text-h6 mb-4">Exercise 18. Test</h2>
        
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
        ex1: [],
        ex2: [],
        ex3: [],
        ex4: [],
        ex5: [],
        ex6: [],
        ex7: [],
        ex8: [],
        ex9: [],
        ex10: [],
        ex11: {
          a: '',
          b: '',
          c: '',
          d: '',
          e: ''
        },
        ex12: [],
        ex13_1: null,
        ex13_2: null,
        ex14: [],
        ex15_1: null,
        ex15_2: null,
        ex15_3: null,
        ex15_4: null,
        ex15_5: null,
        ex15_6: null,
        ex15_7: null,
        ex16_1: [],
        ex16_2: [],
        ex17: [],
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
      definitionExercises: [
        {
          word: "Friendly",
          options: [
            "Always smiles and is approachable",
            "Often keeps to themselves and avoids conversation",
            "Is indifferent to the feelings of others",
            "Prefers to be alone and rarely engages with others"
          ]
        },
        {
          word: "Creative",
          options: [
            "Enjoys thinking outside the box and making new things",
            "Follows strict rules without any variation",
            "Only works with established ideas and methods",
            "Avoids artistic activities and prefers manual labor"
          ]
        },
        {
          word: "Confident",
          options: [
            "Often feels insecure and doubts their abilities",
            "Believes in their skills and expresses themselves clearly",
            "Frequently seeks approval from others before making decisions",
            "Is shy and avoids leadership roles"
          ]
        },
        {
          word: "Caring",
          options: [
            "Shows concern for others' well-being",
            "Is indifferent to the needs of others",
            "Only focuses on their own interests",
            "Enjoys making fun of others' problems"
          ]
        },
        {
          word: "Charismatic",
          options: [
            "Has a magnetic personality that draws people in",
            "Is uninteresting and rarely engages others",
            "Prefers solitary activities over social gatherings",
            "Often makes others uncomfortable with their presence"
          ]
        },
        {
          word: "Stylish",
          options: [
            "Always dresses in a way that reflects modern trends",
            "Wears mismatched clothes without any consideration",
            "Prefers practical clothing regardless of fashion",
            "Is unconcerned about their appearance"
          ]
        },
        {
          word: "Generous",
          options: [
            "Frequently shares their resources and supports others",
            "Hoards possessions and refuses to share",
            "Only helps when it benefits them personally",
            "Is unaware of others' needs and lacks compassion"
          ]
        }
      ],
      wordAssociation: [
        {
          word: "Outgoing",
          options: ["Friendly", "Reserve", "Sociable"]
        },
        {
          word: "Generous",
          options: ["Selfish", "Kind", "Greedy"]
        },
        {
          word: "Charming",
          options: ["Charismatic", "Awkward", "Attractive"]
        },
        {
          word: "Shy",
          options: ["Introverted", "Confident", "Loud"]
        },
        {
          word: "Elegant",
          options: ["Graceful", "Clumsy", "Stylish"]
        },
        {
          word: "Supportive",
          options: ["Understanding", "Dismissive", "Encouraging"]
        },
        {
          word: "Daring",
          options: ["Fearless", "Cautious", "Bold"]
        }
      ],
      generalMeaning: [
        {
          options: ["Tall", "Slim", "Appearance", "Athletic"]
        },
        {
          options: ["Caring", "Friendly", "Personality", "Rude"]
        },
        {
          options: ["Stylish", "Elegant", "Fashion", "Trendy"]
        },
        {
          options: ["Confident", "Shy", "Character", "Introverted"]
        },
        {
          options: ["Creative", "Imaginative", "Artistic", "Dull"]
        },
        {
          options: ["Generous", "Selfish", "Nature", "Giving"]
        },
        {
          options: ["Charismatic", "Boring", "Charm", "Dull"]
        }
      ],
      translationExercises: [
        {
          phrase: "Tall and slim",
          options: [
            "Высокий и стройный",
            "Маленький и полный",
            "Широкий и крепкий"
          ]
        },
        {
          phrase: "Bright smile",
          options: [
            "Яркая улыбка",
            "Тоскливая улыбка",
            "Неприветливая улыбка"
          ]
        },
        {
          phrase: "Friendly personality",
          options: [
            "Дружелюбный характер",
            "Закрытый характер",
            "Холодный характер"
          ]
        },
        {
          phrase: "Curly hair",
          options: [
            "Прямые волосы",
            "Кудрявые волосы",
            "Короткие волосы"
          ]
        },
        {
          phrase: "Generous nature",
          options: [
            "Щедрая натура",
            "Жадная натура",
            "Упрямая натура"
          ]
        },
        {
          phrase: "Deep blue eyes",
          options: [
            "Светло-зеленые глаза",
            "Темно-карие глаза",
            "Глубокие синие глаза"
          ]
        },
        {
          phrase: "Confident demeanor",
          options: [
            "Уверенное поведение",
            "Неуверенное поведение",
            "Скромное поведение"
          ]
        }
      ],
      quizQuestions: [
        {
          question: "What word describes someone who is very attractive?",
          options: ["Ugly", "Beautiful", "Shy"]
        },
        {
          question: "Which term refers to a person's nature or disposition?",
          options: ["Appearance", "Personality", "Hair"]
        },
        {
          question: "What do you call someone who is always happy and cheerful?",
          options: ["Moody", "Serious", "Joyful"]
        }
      ],
      options: {
        ex15_1: ['Respected', 'slender', 'bloomed'],
        ex15_2: ['Go on trip', 'hang out with', 'do sport'],
        ex15_3: ['Chat online', 'send text', 'do voluntary work'],
        ex15_4: ['Listen to music', 'play games', 'send emails'],
        ex15_5: ['aggressive', 'mean', 'disonest'],
        ex15_6: ['Thoughtful', 'well-meaning', 'decisive'],
        ex15_7: ['Brightened', 'Creative', 'trendy'],
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
        ex1: ["oOo", "Ooo", "ooOoo", "Oooo", "oOoo", "oOo", "oOoo"],
        ex2: ["[ˈpeɪʃnt]", "[ˈʤeləs]", "[dɪsˈɒnɪst]", "[səˈpɔːtɪv]", "[pɜːsəˈnælɪtɪ]", "[ˈkaʊntlɪs]", "[ˈkʌmf(ə)təb(ə)l]"],
        ex3: ["Honest", "Violent", "Caring", "Identity", "Thick", "Crucial", "Thin"],
        ex4: ["Jealous", "Kind", "Blue", "Fast", "Long", "Intelligent"],
        ex5: ["Jealous", "Mean", "Moody"],
        ex6: ["Take care", "Watch"],
        ex7: ["Adjective", "Noun", "Verb", "Verb", "Adjective", "Noun", "Adjective"],
        ex8: [0, 0, 1, 0, 0, 0, 0],
        ex9: [2, 1, 0, 0, 0, 2, 0],
        ex10: [2, 2, 2, 2, 2, 2, 0],
        ex11: {
          a: "a bear with a sore head",
          b: "give the cold shoulder",
          c: "be a pain in the neck",
          d: "get off my back",
          e: "get on nerves"
        },
        ex12: ["Create", "Artistic", "Stylish"],
        ex13: ["Trendy", "sharp"],
        ex14: [0, 0, 0, 1, 0, 2, 0],
        ex15: ["Respected", "hang out with", "Chat online", "play games", "aggressive", "well-meaning", "Creative"],
        ex16: [
          ["What was her outfit like?"],
          ["What was the movie?"]
        ],
        ex17: [1, 1, 2],
        test1: ["kindhearted", "charming", "unique", "athletic", "confident"],
        test2: [
          "being kind and pleasant to others.",
          "having a strong belief in oneself and one's abilities.",
          "being the only one of its kind, unlike anything else.",
          "delightful and pleasing in a way that attracts others.",
          "physically fit and skilled in sports or physical activities."
        ],
        test3: [
          "look very impressive.",
          "want to get to know him better.",
          "achieve their goals.",
          "excels in physical activities.",
          "volunteers in the community.",
          "stand out in any event.",
          "makes everyone laugh."
        ]
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
        ex12: null,
        ex13: null,
        ex14: null,
        ex15: null,
        ex16: null,
        ex17: null
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
        const currentAnswer = this.answers.ex11[targetIdiomKey];
        if (!currentAnswer || currentAnswer !== this.draggedWord) {
          this.$set(this.answers.ex11, targetIdiomKey, 
            currentAnswer ? `${currentAnswer} ${this.draggedWord}` : this.draggedWord);
        }
      }
    },
    
    clearAnswer(field, subfield = null) {
      if (subfield) {
        this.$set(this.answers[field], subfield, '');
      } else {
        this.$set(this.answers, field, Array.isArray(this.answers[field]) ? [] : '');
      }
    },
    
    checkExercise(exercise) {
      if (typeof exercise === 'number') {
        // Для старых упражнений 1-7
        const userAnswers = this.answers[`ex${exercise}`];
        const correctAnswers = this.correctAnswers[`ex${exercise}`];
        this.results[`ex${exercise}`] = JSON.stringify(userAnswers) === JSON.stringify(correctAnswers);
      } else {
        // Для новых упражнений
        const exNum = exercise.replace('ex', '');
        const userAnswers = this.answers[exercise];
        const correctAnswers = this.correctAnswers[exercise];
        
        if (exercise === 'ex11') {
          // Особый случай для упражнения с идиомами
          let allCorrect = true;
          for (const key in correctAnswers) {
            if (userAnswers[key]?.toLowerCase().replace(/\s+/g, ' ') !== 
                correctAnswers[key].toLowerCase()) {
              allCorrect = false;
              break;
            }
          }
          this.results.ex11 = allCorrect;
        } 
        else if (exercise === 'ex13') {
          // Проверка для упражнения 13 (бывшее 10)
          this.results.ex13 = (
            userAnswers._1 === correctAnswers[0] &&
            userAnswers._2 === correctAnswers[1]
          );
        }
        else if (exercise === 'ex16') {
          // Проверка для упражнения 16 (бывшее 12)
          this.results.ex16 = (
            JSON.stringify([...userAnswers._1].sort()) === JSON.stringify([...correctAnswers[0]].sort()) &&
            JSON.stringify([...userAnswers._2].sort()) === JSON.stringify([...correctAnswers[1]].sort())
          );
        }
        else {
          // Стандартная проверка для остальных упражнений
          this.results[exercise] = JSON.stringify(userAnswers) === JSON.stringify(correctAnswers);
        }
      }
    },
    
    checkTest() {
      const testCorrect = (
        this.answers.test1_1 === this.correctAnswers.test1[0] &&
        this.answers.test1_2 === this.correctAnswers.test1[1] &&
        this.answers.test1_3 === this.correctAnswers.test1[2] &&
        this.answers.test1_4 === this.correctAnswers.test1[3] &&
        this.answers.test1_5 === this.correctAnswers.test1[4] &&
        this.answers.test2_1 === this.correctAnswers.test2[0] &&
        this.answers.test2_2 === this.correctAnswers.test2[1] &&
        this.answers.test2_3 === this.correctAnswers.test2[2] &&
        this.answers.test2_4 === this.correctAnswers.test2[3] &&
        this.answers.test2_5 === this.correctAnswers.test2[4] &&
        this.answers.test3_1 === this.correctAnswers.test3[0] &&
        this.answers.test3_2 === this.correctAnswers.test3[1] &&
        this.answers.test3_3 === this.correctAnswers.test3[2] &&
        this.answers.test3_4 === this.correctAnswers.test3[3] &&
        this.answers.test3_5 === this.correctAnswers.test3[4] &&
        this.answers.test3_6 === this.correctAnswers.test3[5] &&
        this.answers.test3_7 === this.correctAnswers.test3[6]
      );
      
      this.testResult = testCorrect;
    }
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