import React, { useState, useEffect } from 'react';
import { ChevronRight, RotateCcw, Trophy, Brain } from 'lucide-react';

const QuizGame = () => {
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [score, setScore] = useState(0);
  const [selectedAnswer, setSelectedAnswer] = useState(null);
  const [showResult, setShowResult] = useState(false);
  const [gameFinished, setGameFinished] = useState(false);
  const [timeLeft, setTimeLeft] = useState(15);
  const [selectedCategory, setSelectedCategory] = useState(null);
  const [questions, setQuestions] = useState([]);

  const questionCategories = {
    teknoloji: {
      name: "💻 Teknoloji",
      color: "from-blue-500 to-cyan-500",
      questions: [
        {
          question: "React'te state güncellemek için hangi hook kullanılır?",
          options: ["useEffect", "useState", "useContext", "useReducer"],
          correct: 1
        },
        {
          question: "JavaScript'te hangi method array'e yeni eleman ekler?",
          options: ["push()", "pop()", "shift()", "slice()"],
          correct: 0
        },
        {
          question: "CSS'te flexbox ile elemanları ortalar hangi property?",
          options: ["align-items: center", "justify-content: center", "text-align: center", "vertical-align: middle"],
          correct: 0
        },
        {
          question: "Python'da liste comprehension söz dizimi hangisidir?",
          options: ["[x for x in list]", "{x for x in list}", "(x for x in list)", "[x in list for x]"],
          correct: 0
        },
        {
          question: "HTTP status code 404 ne anlama gelir?",
          options: ["Server Error", "Not Found", "Unauthorized", "Bad Request"],
          correct: 1
        }
      ]
    },
    spor: {
      name: "⚽ Spor",
      color: "from-green-500 to-emerald-500",
      questions: [
        {
          question: "2022 FIFA Dünya Kupası hangi ülkede düzenlendi?",
          options: ["Rusya", "Brezilya", "Katar", "Almanya"],
          correct: 2
        },
        {
          question: "Basketbolda üç sayılık atış hangi çizginin arkasından yapılır?",
          options: ["Serbest atış çizgisi", "Üç sayılık çizgisi", "Orta saha çizgisi", "Yan çizgi"],
          correct: 1
        },
        {
          question: "Tenis'te bir sette kaç oyun kazanan oyuncu seti alır?",
          options: ["5", "6", "7", "8"],
          correct: 1
        },
        {
          question: "Olimpiyatlarda hangi spor dalında Türkiye en çok madalya kazandı?",
          options: ["Güreş", "Halter", "Boks", "Atletizm"],
          correct: 0
        },
        {
          question: "Futbolda penaltı vuruşu hangi mesafeden yapılır?",
          options: ["10 metre", "11 metre", "12 metre", "13 metre"],
          correct: 1
        }
      ]
    },
    tarih: {
      name: "🏛️ Tarih",
      color: "from-amber-500 to-orange-500",
      questions: [
        {
          question: "Osmanlı İmparatorluğu hangi yılda kuruldu?",
          options: ["1299", "1300", "1301", "1302"],
          correct: 0
        },
        {
          question: "İkinci Dünya Savaşı hangi yılda başladı?",
          options: ["1938", "1939", "1940", "1941"],
          correct: 1
        },
        {
          question: "Türkiye Cumhuriyeti hangi tarihte ilan edildi?",
          options: ["29 Ekim 1922", "29 Ekim 1923", "30 Ağustos 1922", "30 Ağustos 1923"],
          correct: 1
        },
        {
          question: "Fatih Sultan Mehmet İstanbul'u hangi yılda fethetti?",
          options: ["1451", "1452", "1453", "1454"],
          correct: 2
        },
        {
          question: "Atatürk'ün doğum yılı hangisidir?",
          options: ["1880", "1881", "1882", "1883"],
          correct: 1
        }
      ]
    },
    bilim: {
      name: "🔬 Bilim",
      color: "from-purple-500 to-pink-500",
      questions: [
        {
          question: "Suyun kimyasal formülü nedir?",
          options: ["H2O", "CO2", "NaCl", "O2"],
          correct: 0
        },
        {
          question: "Işık hızı saniyede yaklaşık kaç kilometre?",
          options: ["200.000 km", "250.000 km", "300.000 km", "350.000 km"],
          correct: 2
        },
        {
          question: "İnsan vücudunda kaç kemik vardır?",
          options: ["186", "206", "226", "246"],
          correct: 1
        },
        {
          question: "Periyodik tabloda altının sembolü nedir?",
          options: ["Al", "Ag", "Au", "At"],
          correct: 2
        },
        {
          question: "DNA'nın açılımı nedir?",
          options: ["Deoksiribonükleik asit", "Dinamik nükleik asit", "Direkt nükleik asit", "Değişken nükleik asit"],
          correct: 0
        }
      ]
    },
    genel: {
      name: "🌍 Genel Kültür",
      color: "from-teal-500 to-cyan-500",
      questions: [
        {
          question: "Dünyanın en büyük okyanusu hangisidir?",
          options: ["Atlantik", "Hint", "Pasifik", "Arktik"],
          correct: 2
        },
        {
          question: "Mona Lisa tablosunu kim yapmıştır?",
          options: ["Michelangelo", "Leonardo da Vinci", "Picasso", "Van Gogh"],
          correct: 1
        },
        {
          question: "Hangi gezegen Güneş'e en yakındır?",
          options: ["Venüs", "Mars", "Merkür", "Dünya"],
          correct: 2
        },
        {
          question: "Pizza hangi ülkenin yemeğidir?",
          options: ["Fransa", "İspanya", "Yunanistan", "İtalya"],
          correct: 3
        },
        {
          question: "Dünyanın en yüksek dağı hangisidir?",
          options: ["K2", "Everest", "Kilimanjaro", "Elbrus"],
          correct: 1
        }
      ]
    }
  };

  useEffect(() => {
    if (!gameFinished && timeLeft > 0) {
      const timer = setTimeout(() => setTimeLeft(timeLeft - 1), 1000);
      return () => clearTimeout(timer);
    } else if (timeLeft === 0 && !showResult) {
      handleNextQuestion();
    }
  }, [timeLeft, gameFinished, showResult]);

  const handleAnswerClick = (selectedIndex) => {
    if (selectedAnswer !== null) return;
    
    setSelectedAnswer(selectedIndex);
    setShowResult(true);
    
    if (selectedIndex === questions[currentQuestion].correct) {
      setScore(score + 1);
    }
  };

  const handleNextQuestion = () => {
    if (currentQuestion < questions.length - 1) {
      setCurrentQuestion(currentQuestion + 1);
      setSelectedAnswer(null);
      setShowResult(false);
      setTimeLeft(15);
    } else {
      setGameFinished(true);
    }
  };

  const resetGame = () => {
    setCurrentQuestion(0);
    setScore(0);
    setSelectedAnswer(null);
    setShowResult(false);
    setGameFinished(false);
    setTimeLeft(15);
    setSelectedCategory(null);
    setQuestions([]);
  };

  const startQuiz = (categoryKey) => {
    const categoryQuestions = questionCategories[categoryKey].questions;
    setQuestions(categoryQuestions);
    setSelectedCategory(categoryKey);
    setCurrentQuestion(0);
    setScore(0);
    setSelectedAnswer(null);
    setShowResult(false);
    setGameFinished(false);
    setTimeLeft(15);
  };

  // Kategori seçim ekranı
  if (!selectedCategory) {
    return (
      <div className="min-h-screen bg-gradient-to-br from-slate-900 via-gray-900 to-zinc-900 flex items-center justify-center p-4">
        <div className="bg-white/95 backdrop-blur-xl rounded-3xl p-12 max-w-6xl w-full shadow-2xl border border-gray-200">
          <div className="text-center mb-12">
            <div className="bg-gradient-to-r from-emerald-500 to-teal-500 p-4 rounded-full w-20 h-20 mx-auto mb-6 flex items-center justify-center">
              <Brain className="w-10 h-10 text-white" />
            </div>
            <h1 className="text-5xl font-bold text-gray-800 mb-4">Quiz Challenge</h1>
            <p className="text-xl text-gray-600">Bir kategori seçin ve bilginizi test edin!</p>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            {Object.entries(questionCategories).map(([key, category]) => (
              <button
                key={key}
                onClick={() => startQuiz(key)}
                className={`bg-gradient-to-r ${category.color} p-8 rounded-2xl text-white font-bold text-xl transition-all duration-300 transform hover:scale-105 hover:shadow-2xl group`}
              >
                <div className="text-center">
                  <div className="text-4xl mb-4">{category.name.split(' ')[0]}</div>
                  <div className="text-xl mb-4">{category.name.split(' ').slice(1).join(' ')}</div>
                  <div className="text-sm opacity-80 group-hover:opacity-100 transition-opacity">
                    {category.questions.length} Soru
                  </div>
                  <div className="mt-4 bg-white/20 rounded-full px-4 py-2 text-sm">
                    Başla →
                  </div>
                </div>
              </button>
            ))}
          </div>

          <div className="text-center mt-12">
            <div className="bg-gray-100 rounded-2xl p-6 inline-block">
              <h3 className="text-gray-700 font-semibold mb-2">🎯 Nasıl Oynanır?</h3>
              <p className="text-gray-600 text-sm">
                Her soru için 15 saniyeniz var • Doğru cevap yeşil, yanlış kırmızı • Skorunuzu artırın!
              </p>
            </div>
          </div>
        </div>
      </div>
    );
  }

  const getScoreMessage = () => {
    const percentage = (score / questions.length) * 100;
    if (percentage >= 80) return { text: "Mükemmel! 🎉", color: "text-emerald-600" };
    if (percentage >= 60) return { text: "İyi iş! 👍", color: "text-blue-600" };
    if (percentage >= 40) return { text: "Fena değil! 🙂", color: "text-orange-600" };
    return { text: "Biraz daha çalış! 💪", color: "text-red-600" };
  };

  if (gameFinished) {
    const scoreMessage = getScoreMessage();
    const currentCategory = questionCategories[selectedCategory];
    return (
      <div className="min-h-screen bg-gradient-to-br from-slate-900 via-gray-900 to-zinc-900 flex items-center justify-center p-4">
        <div className="bg-white/95 backdrop-blur-xl rounded-3xl p-12 max-w-lg w-full text-center shadow-2xl border border-gray-200">
          <div className={`bg-gradient-to-r ${currentCategory.color} p-4 rounded-full w-24 h-24 mx-auto mb-8 flex items-center justify-center`}>
            <Trophy className="w-12 h-12 text-white" />
          </div>
          <h2 className="text-4xl font-bold text-gray-800 mb-4">Quiz Tamamlandı!</h2>
          <div className="text-sm text-gray-600 mb-4">{currentCategory.name} Kategorisi</div>
          <div className="text-7xl font-black text-transparent bg-gradient-to-r from-emerald-600 to-teal-600 bg-clip-text mb-4">{score}/{questions.length}</div>
          <p className={`text-2xl font-semibold mb-8 ${scoreMessage.color}`}>{scoreMessage.text}</p>
          
          <div className="space-y-4">
            <button
              onClick={() => startQuiz(selectedCategory)}
              className={`bg-gradient-to-r ${currentCategory.color} hover:opacity-90 text-white font-semibold py-4 px-8 rounded-2xl transition-all duration-300 transform hover:scale-105 hover:shadow-lg flex items-center gap-3 mx-auto text-lg mb-4`}
            >
              <RotateCcw className="w-6 h-6" />
              Tekrar Dene
            </button>
            
            <button
              onClick={resetGame}
              className="bg-gray-600 hover:bg-gray-700 text-white font-semibold py-3 px-6 rounded-2xl transition-all duration-300 transform hover:scale-105 hover:shadow-lg flex items-center gap-3 mx-auto"
            >
              Kategori Değiştir
            </button>
          </div>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gradient-to-br from-purple-900 via-blue-900 to-indigo-900 flex items-center justify-center p-4">
      <div className="bg-white/10 backdrop-blur-lg rounded-2xl p-8 max-w-2xl w-full border border-white/20 shadow-2xl">
        {/* Header */}
        <div className="flex justify-between items-center mb-8">
          <div className="flex items-center gap-2">
            <Brain className="w-6 h-6 text-purple-300" />
            <span className="text-white font-semibold">Quiz Oyunu</span>
          </div>
          <div className="text-purple-300 font-semibold">
            Soru {currentQuestion + 1}/{questions.length}
          </div>
        </div>

        {/* Progress Bar */}
        <div className="w-full bg-white/20 rounded-full h-2 mb-6">
          <div 
            className="bg-gradient-to-r from-purple-500 to-pink-500 h-2 rounded-full transition-all duration-500"
            style={{ width: `${((currentQuestion + 1) / questions.length) * 100}%` }}
          ></div>
        </div>

        {/* Timer */}
        <div className="flex justify-center mb-6">
          <div className={`text-2xl font-bold px-4 py-2 rounded-full ${
            timeLeft <= 5 ? 'bg-red-500/20 text-red-300 animate-pulse' : 'bg-white/20 text-white'
          }`}>
            {timeLeft}s
          </div>
        </div>

        {/* Question */}
        <div className="text-center mb-8">
          <h2 className="text-2xl font-bold text-white mb-6 leading-relaxed">
            {questions[currentQuestion].question}
          </h2>
        </div>

        {/* Options */}
        <div className="space-y-4 mb-8">
          {questions[currentQuestion].options.map((option, index) => {
            let buttonClass = "w-full p-4 text-left rounded-xl font-semibold transition-all duration-300 transform hover:scale-105 ";
            
            if (showResult) {
              if (index === questions[currentQuestion].correct) {
                buttonClass += "bg-green-500/30 text-green-200 border-2 border-green-400";
              } else if (index === selectedAnswer) {
                buttonClass += "bg-red-500/30 text-red-200 border-2 border-red-400";
              } else {
                buttonClass += "bg-white/10 text-gray-300 border border-white/20";
              }
            } else {
              buttonClass += "bg-white/10 hover:bg-white/20 text-white border border-white/20 hover:border-white/40";
            }

            return (
              <button
                key={index}
                onClick={() => handleAnswerClick(index)}
                disabled={showResult}
                className={buttonClass}
              >
                <span className="flex items-center justify-between">
                  {option}
                  {showResult && index === questions[currentQuestion].correct && (
                    <span className="text-green-400">✓</span>
                  )}
                  {showResult && index === selectedAnswer && index !== questions[currentQuestion].correct && (
                    <span className="text-red-400">✗</span>
                  )}
                </span>
              </button>
            );
          })}
        </div>

        {/* Next Button */}
        {showResult && (
          <div className="text-center">
            <button
              onClick={handleNextQuestion}
              className="bg-gradient-to-r from-purple-500 to-pink-500 hover:from-purple-600 hover:to-pink-600 text-white font-bold py-3 px-6 rounded-xl transition-all duration-300 transform hover:scale-105 flex items-center gap-2 mx-auto"
            >
              {currentQuestion < questions.length - 1 ? 'Sonraki Soru' : 'Sonuçları Gör'}
              <ChevronRight className="w-5 h-5" />
            </button>
          </div>
        )}

        {/* Score */}
        <div className="text-center mt-6 text-purple-300">
          Mevcut Skor: <span className="font-bold text-white">{score}/{currentQuestion + (showResult ? 1 : 0)}</span>
        </div>
      </div>
    </div>
  );
};

export default QuizGame;