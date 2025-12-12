import React, { useState, useEffect } from 'react';
import { initializeApp } from 'firebase/app';
import { 
  getAuth, 
  signInAnonymously, 
  onAuthStateChanged,
  signInWithCustomToken 
} from 'firebase/auth';
import { 
  getFirestore, 
  collection, 
  addDoc, 
  getDocs, 
  serverTimestamp 
} from 'firebase/firestore';
import { 
  Trophy, 
  Sigma, 
  Medal, 
  ChevronRight,
  BrainCircuit,
  Languages,
  BookOpen,
  GraduationCap,
  Sparkles,
  Bot,
  RotateCcw
} from 'lucide-react';

/* -----------------------------------------------------------------------
  FIREBASE CONFIGURATION
  -----------------------------------------------------------------------
*/
const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const appId = typeof __app_id !== 'undefined' ? __app_id : 'limitmaster-default';
const apiKey = ""; 

/* -----------------------------------------------------------------------
  TRANSLATIONS
  -----------------------------------------------------------------------
*/
const TRANSLATIONS = {
  en: {
    title: "LimitMaster",
    subtitle: "Endless Calculus Challenge",
    start: "Start Journey",
    placeholder_user: "Mathematician Name",
    problem: "Problem",
    score: "Score",
    streak: "Streak",
    correct: "Correct",
    incorrect: "Incorrect",
    loading: "Initializing...",
    leaderboard: "Hall of Fame",
    back: "Return Home",
    submit_score: "Save High Score",
    difficulty_easy: "Easy",
    difficulty_med: "Medium",
    difficulty_hard: "Hard",
    difficulty_extreme: "Extreme",
    summary: "Session Report",
    final_score: "Total Score",
    no_data: "No records found.",
    select: "Select the correct limit:",
    ai_help: "Ask AI Assistant",
    ai_explaining: "Analyzing math...",
    ai_explanation: "Solution Breakdown"
  },
  km: {
    title: "LimitMaster",
    subtitle: "ការប្រកួតគណិតវិទ្យាគ្មានទីបញ្ចប់",
    start: "ចាប់ផ្តើម",
    placeholder_user: "ឈ្មោះបេក្ខជន",
    problem: "លំហាត់ទី",
    score: "ពិន្ទុ",
    streak: "ជាប់គ្នា",
    correct: "ត្រឹមត្រូវ",
    incorrect: "មិនត្រឹមត្រូវ",
    loading: "កំពុងដំណើរការ...",
    leaderboard: "តារាងកិត្តិយស",
    back: "ត្រឡប់ក្រោយ",
    submit_score: "រក្សាទុកពិន្ទុ",
    difficulty_easy: "ងាយ",
    difficulty_med: "មធ្យម",
    difficulty_hard: "លំបាក",
    difficulty_extreme: "លំបាកបំផុត",
    summary: "របាយការណ៍",
    final_score: "ពិន្ទុសរុប",
    no_data: "មិនទាន់មានទិន្នន័យ",
    select: "ជ្រើសរើសចម្លើយដែលត្រឹមត្រូវ:",
    ai_help: "សួរគ្រូជំនួយ (AI)",
    ai_explaining: "កំពុងវិភាគ...",
    ai_explanation: "ការពន្យល់ដំណោះស្រាយ"
  }
};

/* -----------------------------------------------------------------------
  MATH ENGINE
  -----------------------------------------------------------------------
*/
const randInt = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;
const randNonZero = (min, max) => {
  let n = 0;
  while (n === 0) n = randInt(min, max);
  return n;
};
const gcd = (x, y) => (!y ? x : gcd(y, x % y));

const shuffle = (array) => {
  let currentIndex = array.length, randomIndex;
  while (currentIndex !== 0) {
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex--;
    [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
  }
  return array;
};

const fmtFrac = (num, den) => {
  if (den < 0) { num = -num; den = -den; }
  if (den === 1) return num.toString();
  const common = gcd(Math.abs(num), Math.abs(den));
  return `${num/common}/${den/common}`;
};

const generateProblem = (level) => {
  let difficulty = 'easy';
  let types = [];
  let points = 10;

  if (level <= 5) {
    difficulty = 'easy';
    types = ['direct_sub', 'simple_inf'];
    points = 10;
  } else if (level <= 15) {
    difficulty = 'med';
    types = ['poly_fraction_0_0', 'poly_inf_inf'];
    points = 20;
  } else if (level <= 25) {
    difficulty = 'hard';
    types = ['conjugate', 'trig_basic'];
    points = 50;
  } else {
    difficulty = 'extreme';
    types = ['euler_limit', 'trig_compound', 'lhopital_log'];
    points = 100;
  }

  const type = types[Math.floor(Math.random() * types.length)];
  
  let p = {
    id: Math.random().toString(36).substr(2, 9),
    type,
    params: {},
    options: [], 
    displayAnswer: '',
    difficulty,
    points,
    latexString: ''
  };

  let correctLabel = "";
  let distractors = [];

  switch (type) {
    case 'direct_sub': 
       {
         const a = randInt(1, 5);
         const k = randInt(1, 10);
         // Format func string with ^ for parser
         p.params = { lim: a, func: `x^2 + ${k}` };
         const ans = a*a + k;
         correctLabel = ans.toString();
         distractors = [(a*a-k).toString(), (2*a+k).toString(), (0).toString()];
         p.latexString = `\\lim_{x \\to ${a}} (x^2 + ${k})`;
       }
       break;
    
    case 'simple_inf': 
       {
         const k = randInt(1, 3);
         p.params = { lim: '∞', num: '1', den: `x^${k}` };
         correctLabel = "0";
         distractors = ["1", "∞", "-∞"];
         p.latexString = `\\lim_{x \\to \\infty} \\frac{1}{x^${k}}`;
       }
       break;

    case 'poly_fraction_0_0':
       {
         const a = randNonZero(2, 6);
         p.params = { lim: a, num_latex: `x^2 - ${a*a}`, den_latex: `x - ${a}` };
         const ans = 2*a;
         correctLabel = ans.toString();
         distractors = [(a).toString(), (a*a).toString(), "0"];
         p.latexString = `\\lim_{x \\to ${a}} \\frac{x^2 - ${a*a}}{x - ${a}}`;
       }
       break;

    case 'poly_inf_inf':
      {
        const a = randNonZero(2, 9);
        const c = randNonZero(2, 9);
        p.params = { lim: '∞', num_latex: `${a}x + ${randInt(1,9)}`, den_latex: `${c}x - ${randInt(1,9)}` };
        correctLabel = fmtFrac(a, c);
        distractors = [fmtFrac(c, a), "0", "∞"];
        p.latexString = `\\lim_{x \\to \\infty} \\frac{${a}x + ...}{${c}x - ...}`;
      }
      break;

    case 'conjugate':
      {
        const a = randInt(1, 1) === 1 ? 4 : 9;
        const sqrtA = Math.sqrt(a);
        p.params = { lim: 0, k: a, sqrtK: sqrtA };
        const ansDen = 2 * sqrtA;
        correctLabel = fmtFrac(1, ansDen);
        distractors = [fmtFrac(1, sqrtA), "0", (2*sqrtA).toString()];
        p.latexString = `\\lim_{x \\to 0} \\frac{\\sqrt{x + ${a}} - ${sqrtA}}{x}`;
      }
      break;

    case 'trig_basic':
      {
        const k = randNonZero(3, 9);
        p.params = { lim: 0, k: k };
        correctLabel = k.toString();
        distractors = ["1", "0", (1/k).toFixed(2)];
        p.latexString = `\\lim_{x \\to 0} \\frac{\\sin(${k}x)}{x}`;
      }
      break;

    case 'euler_limit':
      {
        const k = randInt(2, 5);
        p.params = { lim: '∞', k: k };
        correctLabel = `e^${k}`;
        distractors = [`e`, `1`, `∞`];
        p.latexString = `\\lim_{x \\to \\infty} (1 + \\frac{1}{x})^{${k}x}`;
      }
      break;

    case 'trig_compound':
       {
         const k = randNonZero(2, 4);
         p.params = { lim: 0, k: k };
         correctLabel = fmtFrac(k*k, 2);
         distractors = ["0", "1", k.toString()];
         p.latexString = `\\lim_{x \\to 0} \\frac{1 - \\cos(${k}x)}{x^2}`;
       }
       break;

    default: // lhopital_log
       {
         const a = randNonZero(2, 5);
         const b = randNonZero(2, 5);
         p.params = { lim: 0, a: a, b: b };
         p.type = 'lhopital_log';
         correctLabel = fmtFrac(a, b);
         distractors = ["1", "0", fmtFrac(b, a)];
         p.latexString = `\\lim_{x \\to 0} \\frac{\\ln(1+${a}x)}{\\sin(${b}x)}`;
       }
       break;
  }

  p.displayAnswer = correctLabel;
  const opts = [{ id: 'correct', label: correctLabel, isCorrect: true }, ...distractors.map((d, i) => ({ id: `wrong_${i}`, label: d, isCorrect: false }))];
  p.options = shuffle(opts);
  return p;
};

/* -----------------------------------------------------------------------
  LATEX RENDERER COMPONENTS
  -----------------------------------------------------------------------
*/
const LatexFont = ({ children, className = "" }) => (
  <span className={`font-serif tracking-tight ${className}`} style={{ fontFamily: '"Latin Modern Math", "Computer Modern", "Times New Roman", serif' }}>
    {children}
  </span>
);

const Variable = ({ char }) => <i className="font-serif italic mr-[1px]">{char}</i>;

// *** NEW: Text Parser for Powers ***
const TexParser = ({ text }) => {
  if (!text) return null;
  // Splits by superscripts, e.g. "x^2", "x^{2}", "e^k"
  const parts = text.split(/(\^\{.*?\}|\^\d+)/g);
  
  return (
    <>
      {parts.map((part, i) => {
        if (part.startsWith('^')) {
           const exp = part.replace(/^[\^\{]+|\}+$/g, '');
           return <sup key={i} className="text-[0.6em] ml-[1px]">{exp}</sup>;
        }
        return <span key={i}>{parseBaseText(part)}</span>;
      })}
    </>
  );
};

const parseBaseText = (text) => {
    // Italicize variables
    const tokens = text.split(/(sin|cos|tan|ln|log|x|∞|[+\-=])/g);
    return tokens.map((t, j) => {
        if (t === 'x') return <Variable key={j} char="x" />;
        if (t === '∞') return <span key={j} className="mx-1 text-[1.1em]">∞</span>;
        if (['sin','cos','tan','ln','log'].includes(t)) return <span key={j} className="font-serif">{t}</span>;
        return <span key={j} className="font-serif">{t}</span>;
    });
};

const LimitLabel = ({ to, className="text-slate-800" }) => (
  <div className={`flex flex-col items-center mr-4 md:mr-6 ${className}`}>
    <LatexFont className="text-xl md:text-3xl italic">lim</LatexFont>
    <div className="flex items-center text-xs md:text-sm mt-1 border-t border-transparent">
      <Variable char="x" />
      <span className="mx-1">→</span>
      <TexParser text={to.toString()} />
    </div>
  </div>
);

const Fraction = ({ num, den }) => (
  <div className="inline-flex flex-col items-center align-middle mx-2">
    <div className="border-b border-current px-1 md:px-2 pb-0.5 md:pb-1 mb-0.5 md:mb-1 text-center w-full">
      {num}
    </div>
    <div className="text-center w-full px-1 md:px-2">
      {den}
    </div>
  </div>
);

// *** NEW: Cleaner Square Root ***
const SquareRoot = ({ children }) => (
  <span className="inline-flex items-baseline whitespace-nowrap">
    <span className="text-[1.2em] leading-none font-serif mr-[1px] -mb-[2px]">√</span>
    <span className="border-t border-current leading-tight px-0.5">{children}</span>
  </span>
);

const MathRenderer = ({ problem, color = "text-slate-900", size = "text-2xl md:text-4xl" }) => {
  const { type, params } = problem;

  const content = () => {
    if (type === 'direct_sub') {
      return (
         <div className={`flex items-center ${size} ${color}`}>
          <LimitLabel to={params.lim} className={color} />
          <LatexFont>
            (<TexParser text={params.func} />)
          </LatexFont>
        </div>
      );
    }
    if (type === 'simple_inf') {
      return (
        <div className={`flex items-center ${size} ${color}`}>
          <LimitLabel to={params.lim} className={color} />
          <Fraction num={<TexParser text={params.num} />} den={<TexParser text={params.den} />} />
        </div>
      );
    }
    if (type === 'poly_fraction_0_0' || type === 'poly_inf_inf') {
      return (
        <div className={`flex items-center ${size} ${color}`}>
          <LimitLabel to={params.lim} className={color} />
          <Fraction num={<TexParser text={params.num_latex} />} den={<TexParser text={params.den_latex} />} />
        </div>
      );
    }
    if (type === 'conjugate') {
      return (
        <div className={`flex items-center ${size} ${color}`}>
          <LimitLabel to="0" className={color} />
          <Fraction 
            num={
              <div className="flex items-center">
                <SquareRoot>
                  <TexParser text={`x + ${params.k}`} />
                </SquareRoot>
                <span className="mx-2 md:mx-3">-</span>
                <TexParser text={params.sqrtK.toString()} />
              </div>
            }
            den={<Variable char="x"/>}
          />
        </div>
      );
    }
    if (type === 'euler_limit') {
      // (1 + 1/x)^kx
      return (
        <div className={`flex items-center ${size} ${color}`}>
          <LimitLabel to="∞" className={color} />
          <div className="flex items-start">
            <div className="flex items-center mx-1">
              <span className="font-light transform scale-y-125">(</span>
              <LatexFont className="mx-1">1</LatexFont>
              <span className="mx-1">+</span>
              <Fraction num={<LatexFont>1</LatexFont>} den={<Variable char="x"/>} />
              <span className="font-light transform scale-y-125">)</span>
            </div>
            <sup className="text-[0.6em] md:text-[0.5em] mt-1 md:mt-2 ml-0.5 font-serif">
              {params.k}<Variable char="x"/>
            </sup>
          </div>
        </div>
      );
    }
    if (type === 'trig_compound') {
       return (
        <div className={`flex items-center ${size} ${color}`}>
          <LimitLabel to="0" className={color} />
          <Fraction 
            num={<LatexFont>1 - cos({params.k}<Variable char="x"/>)</LatexFont>}
            den={<LatexFont><Variable char="x"/><sup className="text-[0.6em]">2</sup></LatexFont>}
          />
        </div>
       );
    }
    if (type === 'lhopital_log') {
       return (
        <div className={`flex items-center ${size} ${color}`}>
          <LimitLabel to="0" className={color} />
          <Fraction 
            num={<LatexFont>ln(1 + {params.a}<Variable char="x"/>)</LatexFont>}
            den={<LatexFont>sin({params.b}<Variable char="x"/>)</LatexFont>}
          />
        </div>
       );
    }
    // Fallback Trig
    return (
      <div className={`flex items-center ${size} ${color}`}>
        <LimitLabel to="0" className={color} />
        <Fraction 
          num={<LatexFont>sin({params.k}<Variable char="x"/>)</LatexFont>}
          den={<Variable char="x"/>}
        />
      </div>
    );
  };
  return content();
};

const LatexOption = ({ text }) => {
  // Uses the same parser to render options beautifully
  if (text.includes('/')) {
    const [num, den] = text.split('/');
    return (
      <div className="inline-flex flex-col items-center align-middle scale-90">
        <span className="border-b border-current px-1 leading-none"><TexParser text={num}/></span>
        <span className="leading-none"><TexParser text={den}/></span>
      </div>
    );
  }
  return <TexParser text={text} />;
}

/* -----------------------------------------------------------------------
  AI ASSISTANT
  -----------------------------------------------------------------------
*/
const AIAssistant = ({ problem, lang, t }) => {
  const [explanation, setExplanation] = useState(null);
  const [loading, setLoading] = useState(false);

  const askAI = async () => {
    setLoading(true);
    try {
      const userQuery = `Explain step-by-step how to solve this calculus limit problem: ${problem.latexString}. The answer is ${problem.displayAnswer}. Use simple terms and unicode math symbols. Explain why.`;
      
      const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          contents: [{ parts: [{ text: userQuery }] }]
        })
      });

      const result = await response.json();
      const text = result.candidates?.[0]?.content?.parts?.[0]?.text || "AI is taking a coffee break. Try again later.";
      setExplanation(text);
    } catch (e) {
      setExplanation("Could not connect to AI Assistance.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="mt-6 w-full max-w-lg mx-auto">
      {!explanation && !loading && (
        <button 
          onClick={askAI}
          className="flex items-center justify-center gap-2 w-full py-3 bg-purple-50 text-purple-700 rounded-xl border border-purple-200 hover:bg-purple-100 font-bold transition-all shadow-sm"
        >
          <Sparkles className="w-5 h-5" /> {t.ai_help}
        </button>
      )}
      
      {loading && (
        <div className="p-4 bg-slate-50 rounded-xl border border-slate-200 text-slate-500 text-center animate-pulse flex flex-col items-center gap-2">
          <Bot className="w-6 h-6 animate-bounce" />
          {t.ai_explaining}
        </div>
      )}

      {explanation && (
        <div className="bg-white rounded-xl border border-purple-100 shadow-lg overflow-hidden animate-in fade-in slide-in-from-bottom-2">
          <div className="bg-purple-50 p-3 border-b border-purple-100 flex items-center gap-2 text-purple-800 font-bold">
            <Bot className="w-5 h-5" /> {t.ai_explanation}
          </div>
          <div className="p-5 text-sm md:text-base text-slate-700 leading-relaxed whitespace-pre-wrap font-sans">
            {explanation.replace(/\*\*/g, '')}
          </div>
        </div>
      )}
    </div>
  );
};

/* -----------------------------------------------------------------------
  MAIN COMPONENT
  -----------------------------------------------------------------------
*/
export default function LimitMaster() {
  const [lang, setLang] = useState('en');
  const t = TRANSLATIONS[lang];
  const [user, setUser] = useState(null);
  const [gameState, setGameState] = useState('home'); 
  
  const [currentProblem, setCurrentProblem] = useState(null);
  const [problemsSolved, setProblemsSolved] = useState(0);
  const [score, setScore] = useState(0);
  const [streak, setStreak] = useState(0);
  const [username, setUsername] = useState('');
  const [leaderboardData, setLeaderboardData] = useState([]);
  const [loading, setLoading] = useState(true);
  const [submitStatus, setSubmitStatus] = useState('idle');
  const [selectedOptionId, setSelectedOptionId] = useState(null);
  const [isProcessing, setIsProcessing] = useState(false);
  const [showNextBtn, setShowNextBtn] = useState(false);

  useEffect(() => {
    const link = document.createElement('link');
    link.href = "https://fonts.googleapis.com/css2?family=Battambang:wght@400;700&family=Lora:ital,wght@0,400;0,600;1,400&display=swap";
    link.rel = "stylesheet";
    document.head.appendChild(link);
  }, []);

  useEffect(() => {
    const initAuth = async () => {
      if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
        await signInWithCustomToken(auth, __initial_auth_token);
      } else {
        await signInAnonymously(auth);
      }
    };
    initAuth();
    const unsubscribe = onAuthStateChanged(auth, (u) => {
      setUser(u);
      setLoading(false);
      if (u) loadLeaderboard();
    });
    return () => unsubscribe();
  }, []);

  const loadLeaderboard = async () => {
    try {
      const colRef = collection(db, 'artifacts', appId, 'public', 'data', 'leaderboard');
      const snap = await getDocs(colRef);
      const data = snap.docs.map(d => d.data());
      data.sort((a, b) => b.score - a.score);
      setLeaderboardData(data.slice(0, 50)); 
    } catch (err) { console.error(err); }
  };

  const startGame = () => {
    if (!username.trim()) return;
    setProblemsSolved(0);
    setScore(0);
    setStreak(0);
    nextProblem(0);
    setGameState('playing');
  };

  const nextProblem = (solvedCount) => {
    const level = solvedCount + 1;
    const p = generateProblem(level);
    setCurrentProblem(p);
    setSelectedOptionId(null);
    setIsProcessing(false);
    setShowNextBtn(false);
  };

  const handleOptionClick = (option) => {
    if (isProcessing || showNextBtn) return;
    setIsProcessing(true);
    setSelectedOptionId(option.id);

    const isCorrect = option.isCorrect;
    
    setTimeout(() => {
      if (isCorrect) {
         setScore(s => s + currentProblem.points + (streak * 10)); 
         setStreak(s => s + 1);
         setProblemsSolved(c => c + 1);
      } else {
         setStreak(0);
      }
      setShowNextBtn(true);
      setIsProcessing(false);
    }, 600);
  };

  const handleNextClick = () => {
    nextProblem(problemsSolved);
  };

  const endGame = () => setGameState('results');

  const postScore = async () => {
    if (!user || submitStatus === 'done') return;
    setSubmitStatus('submitting');
    try {
      const colRef = collection(db, 'artifacts', appId, 'public', 'data', 'leaderboard');
      await addDoc(colRef, {
        username: username,
        score: score,
        problemsSolved: problemsSolved,
        userId: user.uid,
        timestamp: serverTimestamp()
      });
      setSubmitStatus('done');
      loadLeaderboard();
    } catch (err) { setSubmitStatus('error'); }
  };

  const toggleLang = () => setLang(prev => prev === 'en' ? 'km' : 'en');

  if (loading) return <div className="min-h-screen bg-slate-50 flex items-center justify-center text-blue-900 font-serif">{t.loading}</div>;

  return (
    <div className={`min-h-screen bg-slate-50 text-slate-900 selection:bg-blue-100 ${lang === 'km' ? 'font-[Battambang]' : 'font-[Lora]'}`}>
      
      <header className="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
        <div className="max-w-6xl mx-auto px-4 md:px-6 py-3 md:py-4 flex justify-between items-center">
          <div className="flex items-center gap-3 cursor-pointer group" onClick={() => setGameState('home')}>
            <div className="bg-blue-600 p-2 rounded-lg text-white shadow-md group-hover:bg-blue-700 transition-colors">
              <Sigma className="w-6 h-6" />
            </div>
            <div>
              <h1 className="text-xl font-bold tracking-tight text-slate-900 font-[Lora] leading-none">Limit<span className="text-blue-600">Master</span></h1>
              <p className="text-[10px] text-slate-500 font-sans tracking-widest uppercase">University Edition</p>
            </div>
          </div>
          
          <div className="flex items-center gap-4">
            <button 
              onClick={toggleLang}
              className="hidden md:flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-100 border border-slate-200 hover:border-blue-400 text-xs font-bold tracking-wider text-slate-600 transition-all"
            >
              <Languages className="w-3 h-3" />
              {lang === 'en' ? 'KH' : 'EN'}
            </button>
            {gameState === 'playing' && (
               <button onClick={endGame} className="text-xs font-bold text-red-500 hover:bg-red-50 px-3 py-1 rounded-md border border-transparent hover:border-red-100 transition-colors">
                 Quit
               </button>
            )}
          </div>
        </div>
      </header>

      <main className="max-w-5xl mx-auto px-4 md:px-6 py-8 md:py-12">
        {gameState === 'home' && (
          <div className="animate-in fade-in slide-in-from-bottom-4 duration-700">
            <div className="text-center py-12 md:py-16 space-y-6">
              <div className="inline-flex items-center gap-2 px-4 py-1 rounded-full bg-blue-50 border border-blue-100 text-blue-700 text-xs font-bold tracking-widest uppercase mb-4 shadow-sm">
                <GraduationCap className="w-3 h-3" /> {t.subtitle}
              </div>
              <h2 className="text-5xl md:text-7xl font-bold tracking-tight text-slate-900 font-[Lora] leading-tight">
                Pure <span className="text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-indigo-600">Mathematics</span>
              </h2>
            </div>

            <div className="grid md:grid-cols-2 gap-12 items-start max-w-4xl mx-auto">
              <div className="bg-white rounded-xl p-8 border border-slate-100 shadow-xl relative overflow-hidden group hover:shadow-2xl transition-all duration-300">
                <h3 className="text-xl font-bold text-slate-900 mb-6 flex items-center gap-2">
                  <BookOpen className="w-5 h-5 text-blue-600" />
                  {t.start}
                </h3>
                <div className="space-y-4">
                  <div>
                    <label className="block text-xs font-bold text-slate-400 uppercase tracking-wider mb-2">{t.placeholder_user}</label>
                    <input 
                      type="text" 
                      value={username}
                      onChange={(e) => setUsername(e.target.value)}
                      placeholder={t.placeholder_user}
                      className="w-full bg-slate-50 border border-slate-200 rounded-lg px-4 py-3 text-slate-900 focus:outline-none focus:ring-2 focus:ring-blue-500/50 transition-all font-bold"
                      maxLength={15}
                    />
                  </div>
                  <button 
                    onClick={startGame}
                    className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3.5 rounded-lg transition-all shadow-lg shadow-blue-200 flex items-center justify-center gap-2"
                  >
                    {t.start} <ChevronRight className="w-4 h-4" />
                  </button>
                </div>
              </div>

              <div className="bg-white/80 rounded-xl border border-slate-200 p-6 backdrop-blur-sm">
                <div className="flex justify-between items-center mb-6">
                  <h3 className="font-bold text-slate-800 flex items-center gap-2">
                    <Trophy className="w-4 h-4 text-blue-600" /> {t.leaderboard}
                  </h3>
                </div>
                <div className="space-y-3">
                  {leaderboardData.slice(0, 5).map((entry, idx) => (
                    <div key={idx} className="flex items-center justify-between text-sm group cursor-default">
                      <div className="flex items-center gap-3">
                        <span className={`w-5 h-5 flex items-center justify-center rounded text-[10px] font-bold ${idx < 3 ? 'bg-blue-100 text-blue-700' : 'text-slate-500 bg-slate-100'}`}>
                          {idx + 1}
                        </span>
                        <span className="font-medium text-slate-600 group-hover:text-blue-800 transition-colors">{entry.username}</span>
                      </div>
                      <div className="text-right">
                         <span className="font-mono text-blue-600 font-bold block leading-none">{entry.score}</span>
                         <span className="text-[10px] text-slate-400">Solved: {entry.problemsSolved || 0}</span>
                      </div>
                    </div>
                  ))}
                  {leaderboardData.length === 0 && <div className="text-center text-slate-400 text-sm py-4">{t.no_data}</div>}
                </div>
              </div>
            </div>
          </div>
        )}

        {gameState === 'playing' && currentProblem && (
          <div className="max-w-3xl mx-auto animate-in zoom-in-95 duration-500 pb-20">
            <div className="flex justify-between items-end mb-8 border-b border-slate-200 pb-4">
              <div>
                <div className="text-xs font-bold text-slate-400 uppercase tracking-widest mb-1">{t.problem} {problemsSolved + 1}</div>
                <div className={`inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-[10px] font-bold uppercase tracking-wider ${
                    currentProblem.difficulty === 'easy' ? 'bg-emerald-50 text-emerald-600' :
                    currentProblem.difficulty === 'med' ? 'bg-blue-50 text-blue-600' :
                    currentProblem.difficulty === 'hard' ? 'bg-orange-50 text-orange-600' :
                    'bg-purple-50 text-purple-600'
                }`}>
                  <BrainCircuit className="w-3 h-3"/>
                  {t[`difficulty_${currentProblem.difficulty}`]}
                </div>
              </div>
              <div className="flex gap-6 text-right">
                 <div>
                    <div className="text-xs font-bold text-slate-400 uppercase tracking-widest mb-1">{t.streak}</div>
                    <div className="text-xl font-mono text-orange-500 leading-none">{streak} <span className="text-sm text-orange-300">🔥</span></div>
                 </div>
                 <div>
                    <div className="text-xs font-bold text-slate-400 uppercase tracking-widest mb-1">{t.score}</div>
                    <div className="text-xl font-mono text-blue-600 leading-none">{score}</div>
                 </div>
              </div>
            </div>

            <div className="bg-white rounded-2xl p-8 md:p-12 border border-slate-100 shadow-xl flex flex-col items-center justify-center min-h-[300px] mb-8 relative overflow-hidden">
               <div className="transform scale-110 md:scale-125 transition-transform duration-500">
                 <MathRenderer problem={currentProblem} color="text-slate-900" />
               </div>
            </div>

            {!showNextBtn ? (
                <>
                  <div className="text-center text-sm text-slate-500 mb-4 font-bold tracking-wide">{t.select}</div>
                  <div className="grid grid-cols-2 gap-4">
                    {currentProblem.options.map((option) => {
                        let baseStyle = "h-20 rounded-xl border-2 text-xl font-serif transition-all duration-200 flex items-center justify-center shadow-sm hover:shadow-md active:scale-95";
                        let stateStyle = "bg-white border-slate-200 hover:border-blue-400 hover:bg-blue-50 text-slate-800";
                        
                        if (selectedOptionId === option.id) {
                            if (option.isCorrect) stateStyle = "bg-emerald-50 border-emerald-500 text-emerald-800 ring-2 ring-emerald-200";
                            else stateStyle = "bg-rose-50 border-rose-500 text-rose-800 ring-2 ring-rose-200";
                        }
                        return (
                        <button
                            key={option.id}
                            onClick={() => handleOptionClick(option)}
                            disabled={isProcessing}
                            className={`${baseStyle} ${stateStyle}`}
                        >
                            <LatexFont className="text-2xl"><LatexOption text={option.label} /></LatexFont>
                        </button>
                        )
                    })}
                  </div>
                </>
            ) : (
                <div className="space-y-6 animate-in slide-in-from-bottom-4">
                    <div className={`p-4 rounded-xl border text-center font-bold ${currentProblem.options.find(o=>o.id===selectedOptionId)?.isCorrect ? 'bg-emerald-50 border-emerald-200 text-emerald-700' : 'bg-rose-50 border-rose-200 text-rose-700'}`}>
                        {currentProblem.options.find(o=>o.id===selectedOptionId)?.isCorrect ? t.correct : t.incorrect}
                        {!currentProblem.options.find(o=>o.id===selectedOptionId)?.isCorrect && (
                            <div className="mt-2 text-sm font-normal text-slate-600">
                                Answer: <span className="font-mono font-bold"><LatexOption text={currentProblem.displayAnswer} /></span>
                            </div>
                        )}
                    </div>
                    
                    <div className="flex flex-col gap-3">
                         <button 
                            onClick={handleNextClick}
                            className="w-full py-4 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-xl shadow-lg transition-all flex items-center justify-center gap-2"
                         >
                            Next Problem <ChevronRight className="w-5 h-5" />
                         </button>
                         <AIAssistant problem={currentProblem} lang={lang} t={t} />
                    </div>
                </div>
            )}
          </div>
        )}

        {gameState === 'results' && (
          <div className="max-w-2xl mx-auto space-y-8 animate-in slide-in-from-bottom-8 duration-500 text-center">
            <div className="bg-white rounded-2xl p-10 border border-slate-100 shadow-2xl">
              <Trophy className="w-16 h-16 text-blue-600 mx-auto mb-6" />
              <h2 className="text-3xl font-bold text-slate-900 mb-2 font-[Lora]">{t.summary}</h2>
              <div className="text-sm text-slate-400 mb-8">{t.final_score}</div>
              <div className="text-7xl font-mono font-bold text-transparent bg-clip-text bg-gradient-to-br from-blue-500 to-indigo-700 mb-8">
                {score}
              </div>
              <div className="text-slate-500 font-bold">Solved: {problemsSolved}</div>
            </div>

            <div className="flex gap-4 justify-center">
              <button 
                onClick={() => setGameState('home')}
                className="px-8 py-3 rounded-lg border border-slate-300 text-slate-600 hover:bg-slate-50 font-bold transition-all flex items-center gap-2"
              >
                <RotateCcw className="w-4 h-4" /> {t.back}
              </button>
              
              {submitStatus !== 'done' ? (
                 <button 
                   onClick={postScore}
                   disabled={submitStatus === 'submitting'}
                   className="px-8 py-3 rounded-lg bg-blue-600 hover:bg-blue-700 text-white font-bold transition-all shadow-lg shadow-blue-200 flex items-center gap-2"
                 >
                   {submitStatus === 'submitting' ? t.loading : t.submit_score}
                 </button>
              ) : (
                 <button 
                   onClick={() => { setGameState('home'); loadLeaderboard(); }}
                   className="px-8 py-3 rounded-lg bg-emerald-50 text-emerald-600 border border-emerald-200 font-bold transition-all flex items-center gap-2"
                 >
                   {t.leaderboard} <ChevronRight className="w-4 h-4" />
                 </button>
              )}
            </div>
          </div>
        )}
      </main>
    </div>
  );
}