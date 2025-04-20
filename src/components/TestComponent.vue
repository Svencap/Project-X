<template>
    <v-container>
      <v-card class="pa-6">
        <h1 class="text-h4 mb-6">English Exercises</h1>
        
        <!-- Exercise 1 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 1. Choose the correct pronunciation of the word "patient":</h2>
          <v-radio-group v-model="answers.ex1">
            <v-radio label="[ˈpeɪʃnt]" value="a"></v-radio>
            <v-radio label="[peɪnt]" value="b"></v-radio>
            <v-radio label="[paɪnt]" value="c"></v-radio>
          </v-radio-group>
        </v-card>
        
        <!-- Exercise 2 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 2. Find a synonym for the word "trusting":</h2>
          <v-radio-group v-model="answers.ex2">
            <v-radio label="Calm" value="a"></v-radio>
            <v-radio label="Honest" value="b"></v-radio>
            <v-radio label="Admired" value="c"></v-radio>
          </v-radio-group>
        </v-card>
        
        <!-- Exercise 3 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 3. Choose an extra word in each row: Supporting, Caring, Jealous, Creative, Well-meaning.</h2>
          <v-radio-group v-model="answers.ex3">
            <v-radio label="Supporting" value="a"></v-radio>
            <v-radio label="Caring" value="b"></v-radio>
            <v-radio label="Jealous" value="c"></v-radio>
            <v-radio label="Creative" value="d"></v-radio>
            <v-radio label="Well-meaning" value="e"></v-radio>
          </v-radio-group>
        </v-card>
        
        <!-- Exercise 4 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 4. Choose all the adjectives that have a negative meaning:</h2>
          <v-checkbox v-model="answers.ex4" label="Jealous" value="a"></v-checkbox>
          <v-checkbox v-model="answers.ex4" label="Mean" value="b"></v-checkbox>
          <v-checkbox v-model="answers.ex4" label="Trusting" value="c"></v-checkbox>
          <v-checkbox v-model="answers.ex4" label="Moody" value="d"></v-checkbox>
          <v-checkbox v-model="answers.ex4" label="Caring" value="e"></v-checkbox>
        </v-card>
        
        <!-- Exercise 5 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 5. Choose synonyms for the word "look after":</h2>
          <v-checkbox v-model="answers.ex5" label="Take care" value="a"></v-checkbox>
          <v-checkbox v-model="answers.ex5" label="Be careful" value="b"></v-checkbox>
          <v-checkbox v-model="answers.ex5" label="Watch" value="c"></v-checkbox>
          <v-checkbox v-model="answers.ex5" label="Hope" value="d"></v-checkbox>
          <v-checkbox v-model="answers.ex5" label="Expect" value="e"></v-checkbox>
        </v-card>
        
        <!-- Exercise 6 - Drag and Drop Idioms -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 6. Drag words to form idioms:</h2>
          
          <div v-for="(idiom, idiomKey) in idiomExercises" :key="idiomKey" class="mb-8">
            <h3 class="subtitle-1 mb-2">{{ idiomKey.toUpperCase() }})</h3>
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
              <div v-if="!answers[`ex6${idiomKey}`]" class="placeholder-text">
                Drop words here to form the idiom
              </div>
              <div v-else class="idiom-text">
                {{ answers[`ex6${idiomKey}`] }}
              </div>
            </div>
            <v-btn 
              small 
              @click="clearAnswer(`ex6${idiomKey}`)" 
              class="mt-2 clear-btn"
              :disabled="!answers[`ex6${idiomKey}`]"
            >
              Clear
            </v-btn>
          </div>
        </v-card>
        
        <!-- Exercise 7 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 7. Match as many adjectives and verbs as possible to one noun "designer"</h2>
          <v-checkbox v-model="answers.ex7" label="Fashion" value="a"></v-checkbox>
          <v-checkbox v-model="answers.ex7" label="Top" value="b"></v-checkbox>
          <v-checkbox v-model="answers.ex7" label="Invent" value="c"></v-checkbox>
          <v-checkbox v-model="answers.ex7" label="Create sketches" value="d"></v-checkbox>
          <v-checkbox v-model="answers.ex7" label="Bloomed" value="e"></v-checkbox>
          <v-checkbox v-model="answers.ex7" label="Sell" value="f"></v-checkbox>
          <v-checkbox v-model="answers.ex7" label="Draw" value="g"></v-checkbox>
        </v-card>
        
        <!-- Exercise 8 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 8. Fill in the gaps in the text:</h2>
          <p class="mb-4">
            Once upon a time in a quirky little town, there lived a 
            <v-select v-model="answers.ex8_1" :items="options.ex8_1" class="d-inline-block" style="width: 150px;"></v-select>
            artist named Mia. She had a 
            <v-select v-model="answers.ex8_2" :items="options.ex8_2" class="d-inline-block" style="width: 150px;"></v-select>
            sense of humor that often turned mundane moments into 
            <v-select v-model="answers.ex8_3" :items="options.ex8_3" class="d-inline-block" style="width: 150px;"></v-select>
            masterpieces. One day, while being 
            <v-select v-model="answers.ex8_4" :items="options.ex8_4" class="d-inline-block" style="width: 150px;"></v-select>
            about her next project, she decided to create a mural that captured both the joy and sorrow of life. Her 
            <v-select v-model="answers.ex8_5" :items="options.ex8_5" class="d-inline-block" style="width: 150px;"></v-select>
            spirit sparked inspiration in everyone around her, reminding them that art has the power to transform even the most ordinary experiences.
          </p>
        </v-card>

        <!-- Exercise 9 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 9. Choose the correct accent of the word "personality":</h2>
          <v-radio-group v-model="answers.ex9">
            <v-radio label="oooOo" value="a"></v-radio>
            <v-radio label="Ooooo" value="b"></v-radio>
            <v-radio label="ooOoo" value="c"></v-radio>
            <v-radio label="ooooO" value="d"></v-radio>
            <v-radio label="Ooooo" value="e"></v-radio>
          </v-radio-group>
        </v-card>


        <!-- Exercise 10 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 10. Choose one of the two words to complete the phrase:</h2>

          <div class="mb-4">
            <h3 class="subtitle-1 mb-2">Fashion ___</h3>
            <v-radio-group v-model="answers.ex10_1">
              <v-radio label="Trendy" value="a"></v-radio>
              <v-radio label="Well-dressed" value="b"></v-radio>
            </v-radio-group>
          </div>

          <div class="mb-4">
            <h3 class="subtitle-1 mb-2">Eyes ___</h3>
            <v-radio-group v-model="answers.ex10_2">
              <v-radio label="comical" value="a"></v-radio>
              <v-radio label="sharp" value="b"></v-radio>
            </v-radio-group>
          </div>
        </v-card>


        <!-- Exercise 11 -->
        <v-card outlined class="mb-6 pa-4">
          <h2 class="text-h6 mb-4">Exercise 11. Put questions to the highlighted words:</h2>
          <p class="mb-4">
            <strong>Her outfit was incredibly trendy</strong>, making her the center of attention at the party.
          </p>
          <v-checkbox v-model="answers.ex11_1" label="What was her outfit like?" value="a"></v-checkbox>
          <v-checkbox v-model="answers.ex11_1" label="Whose outfit was trendy?" value="b"></v-checkbox>
          <v-checkbox v-model="answers.ex11_1" label="What made her the center of attention at the party?" value="c"></v-checkbox>
          
          <p class="mb-4 mt-6">
            <strong>The movie was surprisingly comical</strong>, providing a much-needed laugh after a long week.
          </p>
          <v-checkbox v-model="answers.ex11_2" label="Was the movie comical?" value="a"></v-checkbox>
          <v-checkbox v-model="answers.ex11_2" label="Why did the movie make you laugh?" value="b"></v-checkbox>
          <v-checkbox v-model="answers.ex11_2" label="What was the movie?" value="c"></v-checkbox>
        </v-card>
        
        <v-btn color="primary" @click="checkAnswers" large class="check-btn">Check Answers</v-btn>
        
        <v-dialog v-model="resultsDialog" width="500">
          <v-card>
            <v-card-title class="text-h5">Your Results</v-card-title>
            <v-card-text>
              <div v-for="(result, index) in results" :key="index">
                <p :class="result.correct ? 'success--text' : 'error--text'">
                  Exercise {{ index + 1 }}: {{ result.correct ? 'Correct' : 'Incorrect' }}
                </p>
              </div>
              <p class="text-h6 mt-4">Total score: {{ score }}/8</p>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="resultsDialog = false">Close</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-card>
    </v-container>
  </template>
  
  <script>
  export default {
    data() {
      return {
        answers: {
          ex1: null,
          ex2: null,
          ex3: null,
          ex4: [],
          ex5: [],
          ex6a: '',
          ex6b: '',
          ex6c: '',
          ex6d: '',
          ex6e: '',
          ex7: [],
          ex8_1: null,
          ex8_2: null,
          ex8_3: null,
          ex8_4: null,
          ex8_5: null,
          ex9: null,
          ex10_1: null,
          ex10_2: null,
          ex11_1: [],
          ex11_2: []
        },
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
          ex8_1: ['Respected', 'slender', 'bloomed'],
          ex8_2: ['aggressive', 'mean', 'comical'],
          ex8_3: ['disonest', 'thoughtful', 'masterpieces'],
          ex8_4: ['dedicated', 'moody', 'decisive'],
          ex8_5: ['Brightened', 'Creative', 'trendy']
        },
        correctAnswers: {
          ex1: 'a',
          ex2: 'b',
          ex3: 'c',
          ex4: ['a', 'b', 'd'],
          ex5: ['a', 'c'],
          ex6a: 'a bear with a sore head',
          ex6b: 'give the cold shoulder',
          ex6c: 'be a pain in the neck',
          ex6d: 'get off my back',
          ex6e: 'get on nerves',
          ex7: ['a', 'b', 'c', 'd', 'f', 'g'],
          ex8_1: 'Respected',
          ex8_2: 'comical',
          ex8_3: 'thoughtful',
          ex8_4: 'dedicated',
          ex8_5: 'Creative',
          ex9: 'c', // ooOoo
          ex10_1: 'a', // Fashion Trendy
          ex10_2: 'b',  // Eyes sharp
          ex11_1: ['a'],
          ex11_2: ['c']
        },
        results: [],
        score: 0,
        resultsDialog: false,
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
      
      checkAnswers() {
        this.results = [];
        this.score = 0;

        const exercises = [
          // Exercise 1
          this.answers.ex1 === this.correctAnswers.ex1,
          // Exercise 2
          this.answers.ex2 === this.correctAnswers.ex2,
          // Exercise 3
          this.answers.ex3 === this.correctAnswers.ex3,
          // Exercise 4
          JSON.stringify([...this.answers.ex4].sort()) === JSON.stringify(this.correctAnswers.ex4.sort()),
          // Exercise 5
          JSON.stringify([...this.answers.ex5].sort()) === JSON.stringify(this.correctAnswers.ex5.sort()),
          // Exercise 6
          this.checkIdiomAnswers(),
          // Exercise 7
          JSON.stringify([...this.answers.ex7].sort()) === JSON.stringify(this.correctAnswers.ex7.sort()),
          // Exercise 8
          this.answers.ex8_1 === this.correctAnswers.ex8_1 &&
          this.answers.ex8_2 === this.correctAnswers.ex8_2 &&
          this.answers.ex8_3 === this.correctAnswers.ex8_3 &&
          this.answers.ex8_4 === this.correctAnswers.ex8_4 &&
          this.answers.ex8_5 === this.correctAnswers.ex8_5,
          // Exercise 9
          this.answers.ex9 === this.correctAnswers.ex9,
          // Exercise 10
          this.answers.ex10_1 === this.correctAnswers.ex10_1 &&
          this.answers.ex10_2 === this.correctAnswers.ex10_2,
          // Exercise 11
          JSON.stringify([...this.answers.ex11_1].sort()) === JSON.stringify(this.correctAnswers.ex11_1.sort()) &&
          JSON.stringify([...this.answers.ex11_2].sort()) === JSON.stringify(this.correctAnswers.ex11_2.sort())
        ];
        
        exercises.forEach(correct => {
          this.results.push({ correct });
          if (correct) this.score++;
        });
        
        this.resultsDialog = true;
      },
      
      checkIdiomAnswers() {
        return (
          this.answers.ex6a.toLowerCase() === this.correctAnswers.ex6a.toLowerCase() &&
          this.answers.ex6b.toLowerCase() === this.correctAnswers.ex6b.toLowerCase() &&
          this.answers.ex6c.toLowerCase() === this.correctAnswers.ex6c.toLowerCase() &&
          this.answers.ex6d.toLowerCase() === this.correctAnswers.ex6d.toLowerCase() &&
          this.answers.ex6e.toLowerCase() === this.correctAnswers.ex6e.toLowerCase()
        );
      }
    }
  }
  </script>
  
  <style lang="scss">
  .drop-zone {
    min-height: 60px;
    border: 2px dashed #bdbdbd;
    border-radius: 4px;
    padding: 12px;
    margin-top: 8px;
    background-color: #424242;
    transition: all 0.5s;
  }
  
  .drop-zone:hover {
    background-color: #eeeeee;
    color: #111;
  }
  
  .placeholder-text {
    color: #9e9e9e;
    font-style: italic;
    text-align: center;
  }
  
  .idiom-text {
    font-weight: 500;
    text-align: center;
  }
  
  .draggable-chip {
    cursor: grab;
    user-select: none;
    transition: all 0.2s;
  }
  
  .draggable-chip:active {
    cursor: grabbing;
    transform: scale(1.05);
    box-shadow: 0 3px 5px rgba(0,0,0,0.2);
  }
  
  .clear-btn {
    transition: all 0.3s;
  }
  
  .check-btn {
    margin-top: 20px;
  }
  
  .success--text {
    color: #4CAF50;
    font-weight: 500;
  }
  
  .error--text {
    color: #F44336;
    font-weight: 500;
  }
  
  .v-card {
    transition: all 0.3s;
  }
  
  .v-card:hover {
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  }
  </style>