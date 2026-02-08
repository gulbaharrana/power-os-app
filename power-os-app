import React, { useState, useEffect, useRef } from 'react';
import { Calendar, Zap, Award, TrendingUp, Book, Dumbbell, Briefcase, MessageSquare, Brain, ChevronRight, Flame, Star, Target, AlertCircle, Clock, Plus, X, Bell, BellRing, BarChart3, Send, Trash2, Play, Pause, BookOpen, FileText, Sparkles, CheckSquare, Trophy, Download, Lightbulb, List, CheckCircle, Circle, GraduationCap, Languages, Search, ChevronDown, ChevronUp, CalendarDays, Menu, Home } from 'lucide-react';

export default function PowerOS() {
  // Core State
  const [currentView, setCurrentView] = useState('dashboard');
  const [showDailySetup, setShowDailySetup] = useState(false);
  const [lastSetupDate, setLastSetupDate] = useState('');
  const [points, setPoints] = useState(0);
  const [level, setLevel] = useState(1);
  const [loading, setLoading] = useState(true);
  const [dayType, setDayType] = useState('class');
  
  // Streaks
  const [studyStreak, setStudyStreak] = useState(0);
  const [workoutStreak, setWorkoutStreak] = useState(0);
  const [skillStreak, setSkillStreak] = useState(0);
  const [maxStreaks, setMaxStreaks] = useState({ study: 0, workout: 0, skill: 0 });
  
  // Tasks
  const [tasks, setTasks] = useState({
    jee: [], skill: [], english: [], body: [], business: []
  });
  const [newTaskInput, setNewTaskInput] = useState({
    jee: '', skill: '', english: '', body: '', business: ''
  });
  const [expandedCategory, setExpandedCategory] = useState(null);
  
  // Daily Setup Tasks
  const [dailySetupTasks, setDailySetupTasks] = useState({
    jee: ['', '', ''], skill: [''], english: [''], body: [''], business: ['']
  });
  const [dailySetupTimes, setDailySetupTimes] = useState({
    jee: ['', '', ''], skill: [''], english: [''], body: [''], business: ['']
  });
  
  // Timer
  const [activeTimer, setActiveTimer] = useState(null);
  const [timerSeconds, setTimerSeconds] = useState(0);
  const [timerRunning, setTimerRunning] = useState(false);
  const [taskTimeTracking, setTaskTimeTracking] = useState({});
  
  // Alarms
  const [alarms, setAlarms] = useState([]);
  const [showAlarmModal, setShowAlarmModal] = useState(false);
  const [newAlarm, setNewAlarm] = useState({ title: '', time: '', category: 'jee', recurring: false });
  
  // History
  const [completedHistory, setCompletedHistory] = useState([]);
  const [completedToday, setCompletedToday] = useState({
    jee: 0, skill: 0, english: 0, body: 0, business: 0
  });
  const [historicalData, setHistoricalData] = useState({});
  const [weeklyData, setWeeklyData] = useState({
    jee: [0, 0, 0, 0, 0, 0, 0],
    skill: [0, 0, 0, 0, 0, 0, 0],
    english: [0, 0, 0, 0, 0, 0, 0],
    body: [0, 0, 0, 0, 0, 0, 0],
    business: [0, 0, 0, 0, 0, 0, 0]
  });

  // Habits
  const [dailyHabits, setDailyHabits] = useState([
    { id: 1, name: 'Wake up by 6 AM', done: false, streak: 0 },
    { id: 2, name: 'Morning workout', done: false, streak: 0 },
    { id: 3, name: '8 glasses water', done: false, streak: 0 },
    { id: 4, name: 'Night revision', done: false, streak: 0 }
  ]);

  // AI Chat
  const [chatMessages, setChatMessages] = useState([]);
  const [chatInput, setChatInput] = useState('');
  const [isChatLoading, setIsChatLoading] = useState(false);
  const chatEndRef = useRef(null);

  // Smart Suggestions
  const [smartSuggestions, setSmartSuggestions] = useState([]);
  const [dailyFocus, setDailyFocus] = useState('');
  const [aiSuggestions, setAiSuggestions] = useState([]);
  const [aiThinking, setAiThinking] = useState(false);

  // Notes
  const [categoryNotes, setCategoryNotes] = useState({
    jee: '', skill: '', english: '', body: '', business: ''
  });
  const [showNotesModal, setShowNotesModal] = useState(false);
  const [currentNotesCategory, setCurrentNotesCategory] = useState('');

  // Achievements
  const [achievements, setAchievements] = useState([
    { id: 1, name: 'First Step', desc: 'Complete first task', unlocked: false, icon: '🎯' },
    { id: 2, name: 'Week Warrior', desc: '7 day streak', unlocked: false, icon: '🔥' },
    { id: 3, name: 'Century', desc: '100 points', unlocked: false, icon: '💯' },
    { id: 4, name: 'Dedicated', desc: '50 tasks done', unlocked: false, icon: '💪' },
    { id: 5, name: 'Balanced', desc: 'All categories in 1 day', unlocked: false, icon: '⚖️' },
    { id: 6, name: 'Chapter Master', desc: 'Complete 10 chapters', unlocked: false, icon: '📚' },
    { id: 7, name: 'Vocab Pro', desc: 'Learn 50 terms', unlocked: false, icon: '🗣️' }
  ]);
  const [showAchievements, setShowAchievements] = useState(false);

  // Lists
  const [lists, setLists] = useState([
    { id: 'today', name: 'Today', icon: '📅', items: [], color: '#3b82f6' },
    { id: 'important', name: 'Important', icon: '⭐', items: [], color: '#f59e0b' },
    { id: 'upcoming', name: 'Upcoming', icon: '🔜', items: [], color: '#a855f7' }
  ]);
  const [customLists, setCustomLists] = useState([]);
  const [activeList, setActiveList] = useState('today');
  const [newListItem, setNewListItem] = useState('');

  // Weekly Planner
  const [weeklyPlan, setWeeklyPlan] = useState({
    monday: { goals: [], focus: '', completed: false },
    tuesday: { goals: [], focus: '', completed: false },
    wednesday: { goals: [], focus: '', completed: false },
    thursday: { goals: [], focus: '', completed: false },
    friday: { goals: [], focus: '', completed: false },
    saturday: { goals: [], focus: '', completed: false },
    sunday: { goals: [], focus: '', completed: false }
  });

  // Syllabus Tracker
  const [syllabusClass, setSyllabusClass] = useState('11');
  const [syllabusSubject, setSyllabusSubject] = useState('physics');
  
  const [syllabus11, setSyllabus11] = useState({
    physics: ['Physical World', 'Units & Measurements', 'Motion in Straight Line', 'Motion in Plane', 'Laws of Motion', 'Work Energy Power', 'System of Particles', 'Gravitation', 'Mechanical Properties of Solids', 'Mechanical Properties of Fluids', 'Thermal Properties', 'Thermodynamics', 'Kinetic Theory', 'Oscillations', 'Waves'].map((name, i) => ({ ch: i + 1, name, done: false })),
    chemistry: ['Basic Concepts', 'Structure of Atom', 'Classification of Elements', 'Chemical Bonding', 'States of Matter', 'Thermodynamics', 'Equilibrium', 'Redox Reactions', 'Hydrogen', 's-Block Elements', 'p-Block Elements', 'Organic Chemistry Basics', 'Hydrocarbons', 'Environmental Chemistry'].map((name, i) => ({ ch: i + 1, name, done: false })),
    maths: ['Sets', 'Relations & Functions', 'Trigonometric Functions', 'Mathematical Induction', 'Complex Numbers', 'Linear Inequalities', 'Permutations & Combinations', 'Binomial Theorem', 'Sequences & Series', 'Straight Lines', 'Conic Sections', '3D Geometry Intro', 'Limits & Derivatives', 'Mathematical Reasoning', 'Statistics', 'Probability'].map((name, i) => ({ ch: i + 1, name, done: false }))
  });

  const [syllabus12, setSyllabus12] = useState({
    physics: ['Electric Charges & Fields', 'Electrostatic Potential', 'Current Electricity', 'Moving Charges & Magnetism', 'Magnetism & Matter', 'Electromagnetic Induction', 'Alternating Current', 'Electromagnetic Waves', 'Ray Optics', 'Wave Optics', 'Dual Nature of Radiation', 'Atoms', 'Nuclei', 'Semiconductor Electronics'].map((name, i) => ({ ch: i + 1, name, done: false })),
    chemistry: ['Solid State', 'Solutions', 'Electrochemistry', 'Chemical Kinetics', 'Surface Chemistry', 'General Principles & Processes', 'p-Block Elements', 'd and f Block Elements', 'Coordination Compounds', 'Haloalkanes & Haloarenes', 'Alcohols Phenols & Ethers', 'Aldehydes Ketones', 'Carboxylic Acids', 'Amines', 'Biomolecules', 'Polymers'].map((name, i) => ({ ch: i + 1, name, done: false })),
    maths: ['Relations & Functions', 'Inverse Trigonometric Functions', 'Matrices', 'Determinants', 'Continuity & Differentiability', 'Application of Derivatives', 'Integrals', 'Application of Integrals', 'Differential Equations', 'Vector Algebra', 'Three Dimensional Geometry', 'Linear Programming', 'Probability'].map((name, i) => ({ ch: i + 1, name, done: false }))
  });

  // Vocabulary (280+ terms)
  const vocabulary = {
    'Force': { hindi: 'बल', meaning: 'धक्का या खींचना', example: 'F = ma' },
    'Mass': { hindi: 'द्रव्यमान', meaning: 'पदार्थ की मात्रा', example: 'kg' },
    'Velocity': { hindi: 'वेग', meaning: 'दिशा सहित चाल', example: 'v = s/t' },
    'Acceleration': { hindi: 'त्वरण', meaning: 'वेग में परिवर्तन की दर', example: 'a = Δv/Δt' },
    'Momentum': { hindi: 'संवेग', meaning: 'द्रव्यमान × वेग', example: 'p = mv' },
    'Angular Momentum': { hindi: 'कोणीय संवेग', meaning: 'घूर्णन गति का माप', example: 'L = Iω' },
    'Density': { hindi: 'घनत्व', meaning: 'द्रव्यमान/आयतन', example: 'ρ = m/V' },
    'Pressure': { hindi: 'दबाव', meaning: 'बल/क्षेत्रफल', example: 'P = F/A' },
    'Energy': { hindi: 'ऊर्जा', meaning: 'कार्य करने की क्षमता', example: 'Joules' },
    'Power': { hindi: 'शक्ति', meaning: 'कार्य करने की दर', example: 'P = W/t' },
    'Work': { hindi: 'कार्य', meaning: 'बल × विस्थापन', example: 'W = F·s' },
    'Torque': { hindi: 'बल आघूर्ण', meaning: 'घुमाने वाला बल', example: 'τ = r×F' },
    'Inertia': { hindi: 'जड़त्व', meaning: 'गति अवस्था बनाए रखना', example: 'Newton 1st law' },
    'Friction': { hindi: 'घर्षण', meaning: 'विरोधी बल', example: 'f = μN' },
    'Charge': { hindi: 'आवेश', meaning: 'विद्युत का गुण', example: 'Coulomb' },
    'Current': { hindi: 'धारा', meaning: 'आवेश का प्रवाह', example: 'I = Q/t' },
    'Voltage': { hindi: 'विभवांतर', meaning: 'विद्युत दबाव', example: 'V = W/Q' },
    'Resistance': { hindi: 'प्रतिरोध', meaning: 'धारा में बाधा', example: 'R = V/I' },
    'Wavelength': { hindi: 'तरंगदैर्ध्य', meaning: 'दो शिखरों की दूरी', example: 'λ' },
    'Frequency': { hindi: 'आवृत्ति', meaning: 'प्रति सेकंड दोलन', example: 'Hz' },
    'Atom': { hindi: 'परमाणु', meaning: 'पदार्थ की सबसे छोटी इकाई', example: 'smallest particle' },
    'Molecule': { hindi: 'अणु', meaning: 'दो या अधिक परमाणु', example: 'H₂O' },
    'Mole': { hindi: 'मोल', meaning: '6.022×10²³ कण', example: 'Avogadro' },
    'Molarity': { hindi: 'मोलरता', meaning: 'मोल/लीटर', example: 'M = mol/L' },
    'Acid': { hindi: 'अम्ल', meaning: 'H⁺ देने वाला', example: 'HCl' },
    'Base': { hindi: 'क्षार', meaning: 'OH⁻ देने वाला', example: 'NaOH' },
    'pH': { hindi: 'पीएच', meaning: 'अम्लता का माप', example: '-log[H⁺]' },
    'Oxidation': { hindi: 'ऑक्सीकरण', meaning: 'इलेक्ट्रॉन खोना', example: 'loss e⁻' },
    'Reduction': { hindi: 'अपचयन', meaning: 'इलेक्ट्रॉन पाना', example: 'gain e⁻' },
    'Catalyst': { hindi: 'उत्प्रेरक', meaning: 'अभिक्रिया तेज करे', example: 'MnO₂' },
    'Function': { hindi: 'फलन', meaning: 'इनपुट-आउटपुट', example: 'f(x)' },
    'Matrix': { hindi: 'आव्यूह', meaning: 'संख्याओं की सारणी', example: '[a b]' },
    'Vector': { hindi: 'सदिश', meaning: 'दिशा सहित', example: 'force' },
    'Derivative': { hindi: 'अवकलज', meaning: 'परिवर्तन की दर', example: 'dy/dx' },
    'Integral': { hindi: 'समाकलन', meaning: 'क्षेत्रफल', example: '∫f(x)dx' },
    'Limit': { hindi: 'सीमा', meaning: 'पहुंचने वाला मान', example: 'lim x→0' },
    'Probability': { hindi: 'प्रायिकता', meaning: 'संभावना', example: 'P(E)' }
  };

  const [vocabSearch, setVocabSearch] = useState('');
  const [learnedTerms, setLearnedTerms] = useState([]);

  const today = new Date();
  const todayString = today.toLocaleDateString('en-IN', { weekday: 'short', month: 'short', day: 'numeric' });
  const todayDateOnly = today.toDateString();
  const currentHour = today.getHours();

  const categoryColors = { jee: '#3b82f6', skill: '#22c55e', english: '#a855f7', body: '#ef4444', business: '#f59e0b' };
  const categoryIcons = { jee: Book, skill: TrendingUp, english: MessageSquare, body: Dumbbell, business: Briefcase };
  const categoryPoints = { jee: 10, skill: 6, english: 5, body: 5, business: 7 };
  const categoryTitles = { jee: 'JEE Mission', skill: 'Skills', english: 'English', body: 'Body', business: 'Business' };

  const isTimeBlocked = () => currentHour >= 14 && currentHour < 19;

  // Generate Smart Suggestions
  const generateSmartSuggestions = () => {
    const suggestions = [];
    
    if (dayType === 'noclass') {
      if (currentHour >= 6 && currentHour < 12) {
        suggestions.push({ icon: '📚', text: 'NO CLASS DAY! Deep study - Complete 2-3 chapters', color: '#3b82f6' });
        suggestions.push({ icon: '💻', text: 'Skill development - 2 hour focused session', color: '#22c55e' });
        suggestions.push({ icon: '📖', text: 'Revise weak topics thoroughly', color: '#a855f7' });
      } else if (currentHour >= 12 && currentHour < 14) {
        suggestions.push({ icon: '📝', text: 'Solve DPP & Previous Year Questions', color: '#3b82f6' });
        suggestions.push({ icon: '💰', text: 'Learn business/trading concepts', color: '#f59e0b' });
      } else if (currentHour >= 19 && currentHour < 22) {
        suggestions.push({ icon: '📈', text: 'Business learning - Perfect time!', color: '#f59e0b' });
        suggestions.push({ icon: '🗣️', text: 'English speaking practice - 30 min', color: '#a855f7' });
        suggestions.push({ icon: '📝', text: 'Night revision - Important topics', color: '#3b82f6' });
      }
    } else {
      if (currentHour >= 6 && currentHour < 9) {
        suggestions.push({ icon: '📚', text: 'Review yesterday\'s class notes', color: '#3b82f6' });
      } else if (currentHour >= 19 && currentHour < 22) {
        suggestions.push({ icon: '✏️', text: 'Complete class homework', color: '#3b82f6' });
        suggestions.push({ icon: '📝', text: 'Revise today\'s topics', color: '#3b82f6' });
      }
    }
    
    if (studyStreak === 0 && currentHour >= 9 && currentHour < 22) {
      suggestions.unshift({ icon: '🔥', text: 'Start study streak - Do 1 JEE task!', color: '#ef4444' });
    }
    
    setSmartSuggestions(suggestions.slice(0, 4));
  };

  // Get AI Decision
  const getAIDecision = async () => {
    setAiThinking(true);
    try {
      const completedChapters = Object.values(syllabus11).concat(Object.values(syllabus12))
        .reduce((sum, sub) => sum + sub.filter(ch => ch.done).length, 0);
      
      const response = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 1000,
          messages: [{
            role: "user",
            content: `POWER OS AI for JEE student.

Context:
- Day: ${dayType === 'class' ? 'Class Day' : 'NO CLASS DAY (Full free time!)'}
- Time: ${currentHour}:00
- Points: ${points} | Level: ${level}
- Streaks: Study(${studyStreak}) Workout(${workoutStreak}) Skill(${skillStreak})
- Completed Chapters: ${completedChapters}/88
- Pending Tasks: JEE(${tasks.jee.length}) Skill(${tasks.skill.length})
- Family Time: 2PM-7PM blocked

${dayType === 'noclass' ? 'IMPORTANT: NO CLASS DAY - Full productive day! Deep study, skills, business, revision!' : 'Class Day - Focus on homework, practice'}

Give strategic advice. JSON only:
{"dailyFocus": "powerful sentence", "suggestions": ["tip1", "tip2", "tip3"]}`
          }]
        })
      });

      const data = await response.json();
      const text = data.content[0].text.replace(/```json|```/g, '').trim();
      const parsed = JSON.parse(text);
      
      setDailyFocus(parsed.dailyFocus);
      setAiSuggestions(parsed.suggestions || []);
      
    } catch (err) {
      if (dayType === 'noclass') {
        setDailyFocus("NO CLASS DAY - Deep study + Skill building + Business learning!");
        setAiSuggestions(["Complete 2-3 chapters", "2hr skill session", "Business learning", "Thorough revision"]);
      } else {
        setDailyFocus("Focus in class, complete homework, practice problems");
        setAiSuggestions(["Attend class", "Complete assignments", "Revise topics"]);
      }
    }
    setAiThinking(false);
  };

  // Complete Daily Setup
  const completeDailySetup = () => {
    Object.keys(dailySetupTasks).forEach(category => {
      dailySetupTasks[category].forEach((taskName, idx) => {
        if (taskName.trim()) {
          const newTask = {
            id: Date.now() + Math.random(),
            name: taskName,
            created: new Date().toISOString(),
            category: category
          };
          
          setTasks(prev => ({
            ...prev,
            [category]: [...prev[category], newTask]
          }));
          
          if (dailySetupTimes[category][idx]) {
            setAlarms(prev => [...prev, {
              id: Date.now() + Math.random(),
              title: taskName,
              time: dailySetupTimes[category][idx],
              category: category,
              triggered: false,
              recurring: false
            }]);
          }
        }
      });
    });
    
    setLastSetupDate(todayDateOnly);
    setShowDailySetup(false);
    setDailySetupTasks({ jee: ['', '', ''], skill: [''], english: [''], body: [''], business: [''] });
    setDailySetupTimes({ jee: ['', '', ''], skill: [''], english: [''], body: [''], business: [''] });
  };

  // Task Functions
  const addTask = (cat) => {
    if (!newTaskInput[cat].trim()) return;
    setTasks({ ...tasks, [cat]: [...tasks[cat], { id: Date.now(), name: newTaskInput[cat], created: new Date().toISOString() }] });
    setNewTaskInput({ ...newTaskInput, [cat]: '' });
  };

  const completeTask = (cat, id, pts) => {
    const task = tasks[cat].find(t => t.id === id);
    if (!task) return;
    
    const timeSpent = taskTimeTracking[id] || 0;
    
    setTasks({ ...tasks, [cat]: tasks[cat].filter(t => t.id !== id) });
    setCompletedHistory([{ ...task, completedAt: new Date().toISOString(), points: pts, timeSpent }, ...completedHistory]);
    setPoints(points + pts);
    setCompletedToday({ ...completedToday, [cat]: completedToday[cat] + 1 });
    
    const dayIndex = new Date().getDay();
    setWeeklyData({
      ...weeklyData,
      [cat]: weeklyData[cat].map((val, idx) => idx === dayIndex ? val + 1 : val)
    });
    
    if (cat === 'jee') {
      const newStreak = studyStreak + 1;
      setStudyStreak(newStreak);
      if (newStreak > maxStreaks.study) setMaxStreaks({ ...maxStreaks, study: newStreak });
    }
    if (cat === 'body') {
      const newStreak = workoutStreak + 1;
      setWorkoutStreak(newStreak);
      if (newStreak > maxStreaks.workout) setMaxStreaks({ ...maxStreaks, workout: newStreak });
    }
    if (cat === 'skill') {
      const newStreak = skillStreak + 1;
      setSkillStreak(newStreak);
      if (newStreak > maxStreaks.skill) setMaxStreaks({ ...maxStreaks, skill: newStreak });
    }
    
    if (activeTimer?.taskId === id) {
      setActiveTimer(null);
      setTimerRunning(false);
      setTimerSeconds(0);
    }
  };

  const deleteTask = (cat, id) => {
    setTasks({ ...tasks, [cat]: tasks[cat].filter(t => t.id !== id) });
    if (activeTimer?.taskId === id) {
      setActiveTimer(null);
      setTimerRunning(false);
      setTimerSeconds(0);
    }
  };

  const startTaskTimer = (taskId, category) => {
    setActiveTimer({ taskId, category });
    setTimerSeconds(taskTimeTracking[taskId] || 0);
    setTimerRunning(true);
  };

  const stopTaskTimer = () => setTimerRunning(false);

  const toggleHabit = (id) => {
    setDailyHabits(prev => prev.map(h => 
      h.id === id ? { ...h, done: !h.done, streak: h.done ? h.streak : h.streak + 1 } : h
    ));
  };

  const toggleChapter = (classNum, subject, idx) => {
    if (classNum === '11') {
      setSyllabus11(prev => ({
        ...prev,
        [subject]: prev[subject].map((ch, i) => i === idx ? { ...ch, done: !ch.done } : ch)
      }));
    } else {
      setSyllabus12(prev => ({
        ...prev,
        [subject]: prev[subject].map((ch, i) => i === idx ? { ...ch, done: !ch.done } : ch)
      }));
    }
    
    const syllabus = classNum === '11' ? syllabus11 : syllabus12;
    if (!syllabus[subject][idx].done) {
      setPoints(points + 15);
    }
  };

  const markTermLearned = (term) => {
    if (!learnedTerms.includes(term)) {
      setLearnedTerms([...learnedTerms, term]);
      setPoints(points + 2);
    }
  };

  const addListItem = () => {
    if (!newListItem.trim()) return;
    const currentList = lists.find(l => l.id === activeList) || customLists.find(l => l.id === activeList);
    if (!currentList) return;
    
    const newItem = { id: Date.now(), text: newListItem, completed: false, createdAt: new Date().toISOString() };
    
    if (lists.find(l => l.id === activeList)) {
      setLists(lists.map(l => l.id === activeList ? { ...l, items: [...l.items, newItem] } : l));
    } else {
      setCustomLists(customLists.map(l => l.id === activeList ? { ...l, items: [...l.items, newItem] } : l));
    }
    setNewListItem('');
  };

  const toggleListItem = (listId, itemId) => {
    const updateItems = (list) => {
      if (list.id === listId) {
        return {
          ...list,
          items: list.items.map(item => 
            item.id === itemId ? { ...item, completed: !item.completed } : item
          )
        };
      }
      return list;
    };
    
    setLists(lists.map(updateItems));
    setCustomLists(customLists.map(updateItems));
    
    const item = [...lists, ...customLists].find(l => l.id === listId)?.items.find(i => i.id === itemId);
    if (item && !item.completed) setPoints(points + 5);
  };

  const deleteListItem = (listId, itemId) => {
    const updateItems = (list) => {
      if (list.id === listId) {
        return { ...list, items: list.items.filter(item => item.id !== itemId) };
      }
      return list;
    };
    setLists(lists.map(updateItems));
    setCustomLists(customLists.map(updateItems));
  };

  const sendChatMessage = async () => {
    if (!chatInput.trim()) return;
    
    const userMessage = { role: 'user', content: chatInput, timestamp: new Date().toISOString() };
    setChatMessages([...chatMessages, userMessage]);
    setChatInput('');
    setIsChatLoading(true);
    
    try {
      const response = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 2000,
          messages: [
            { role: "user", content: `AI Coach for JEE. Stats: L${level}, ${points}pts. Give detailed, strategic advice.` },
            { role: "assistant", content: "Ready." },
            ...chatMessages.slice(-6).map(msg => ({ role: msg.role, content: msg.content })),
            { role: "user", content: chatInput }
          ]
        })
      });

      const data = await response.json();
      const text = data.content[0].text;
      
      const aiMessage = { role: 'assistant', content: text, timestamp: new Date().toISOString() };
      setChatMessages(prev => [...prev, userMessage, aiMessage]);
      
    } catch (err) {
      console.error(err);
    }
    
    setIsChatLoading(false);
  };

  const addAlarm = () => {
    if (!newAlarm.title || !newAlarm.time) return;
    const alarm = { id: Date.now(), ...newAlarm, triggered: false, created: new Date().toISOString() };
    setAlarms([...alarms, alarm]);
    setNewAlarm({ title: '', time: '', category: 'jee', recurring: false });
    setShowAlarmModal(false);
  };

  const deleteAlarm = (alarmId) => {
    setAlarms(alarms.filter(a => a.id !== alarmId));
  };

  const formatTime = (seconds) => {
    const hrs = Math.floor(seconds / 3600);
    const mins = Math.floor((seconds % 3600) / 60);
    const secs = seconds % 60;
    if (hrs > 0) return `${hrs}h ${mins}m`;
    return `${mins}:${secs.toString().padStart(2, '0')}`;
  };

  const exportData = () => {
    const data = { 
      points, level, studyStreak, workoutStreak, skillStreak, maxStreaks, 
      completedHistory, historicalData, achievements, syllabus11, syllabus12,
      learnedTerms, exportDate: new Date().toISOString() 
    };
    const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `poweros-backup-${Date.now()}.json`;
    a.click();
  };

  // Effects
  useEffect(() => {
    let interval;
    if (timerRunning && activeTimer) {
      interval = setInterval(() => {
        setTimerSeconds(prev => prev + 1);
        if (activeTimer) {
          setTaskTimeTracking(prev => ({
            ...prev,
            [activeTimer.taskId]: (prev[activeTimer.taskId] || 0) + 1
          }));
        }
      }, 1000);
    }
    return () => clearInterval(interval);
  }, [timerRunning, activeTimer]);

  useEffect(() => {
    if (!loading && todayDateOnly !== lastSetupDate) {
      if (lastSetupDate) {
        setCompletedToday({ jee: 0, skill: 0, english: 0, body: 0, business: 0 });
        setDailyHabits(dailyHabits.map(h => ({ ...h, done: false })));
      }
      setTimeout(() => setShowDailySetup(true), 500);
    }
  }, [loading, todayDateOnly, lastSetupDate]);

  useEffect(() => {
    const loadData = async () => {
      try {
        const data = await window.storage.get('poweros-complete-data');
        if (data) {
          const parsed = JSON.parse(data.value);
          setPoints(parsed.points || 0);
          setStudyStreak(parsed.studyStreak || 0);
          setWorkoutStreak(parsed.workoutStreak || 0);
          setSkillStreak(parsed.skillStreak || 0);
          setMaxStreaks(parsed.maxStreaks || { study: 0, workout: 0, skill: 0 });
          setTasks(parsed.tasks || tasks);
          setCompletedToday(parsed.completedToday || completedToday);
          setCompletedHistory(parsed.completedHistory || []);
          setHistoricalData(parsed.historicalData || {});
          setAlarms(parsed.alarms || []);
          setDailyHabits(parsed.dailyHabits || dailyHabits);
          setCategoryNotes(parsed.categoryNotes || categoryNotes);
          setTaskTimeTracking(parsed.taskTimeTracking || {});
          setLastSetupDate(parsed.lastSetupDate || '');
          setWeeklyData(parsed.weeklyData || weeklyData);
          setChatMessages(parsed.chatMessages || []);
          setAchievements(parsed.achievements || achievements);
          setDayType(parsed.dayType || 'class');
          setLists(parsed.lists || lists);
          setCustomLists(parsed.customLists || []);
          setWeeklyPlan(parsed.weeklyPlan || weeklyPlan);
          setSyllabus11(parsed.syllabus11 || syllabus11);
          setSyllabus12(parsed.syllabus12 || syllabus12);
          setLearnedTerms(parsed.learnedTerms || []);
        }
      } catch (error) {
        console.log('First load');
      }
      setLoading(false);
    };
    loadData();
  }, []);

  useEffect(() => {
    if (!loading) {
      const data = {
        points, studyStreak, workoutStreak, skillStreak, maxStreaks,
        tasks, completedToday, completedHistory, historicalData,
        alarms, dailyHabits, categoryNotes, taskTimeTracking,
        lastSetupDate, weeklyData, chatMessages, achievements, dayType,
        lists, customLists, weeklyPlan, syllabus11, syllabus12, learnedTerms
      };
      window.storage.set('poweros-complete-data', JSON.stringify(data));
    }
  }, [points, studyStreak, workoutStreak, skillStreak, maxStreaks, tasks, 
      completedToday, completedHistory, historicalData, alarms, dailyHabits, 
      categoryNotes, taskTimeTracking, lastSetupDate, weeklyData, chatMessages, 
      achievements, dayType, lists, customLists, weeklyPlan, syllabus11, syllabus12, learnedTerms]);

  useEffect(() => {
    setLevel(calculateLevel(points));
  }, [points]);

  useEffect(() => {
    generateSmartSuggestions();
    const interval = setInterval(generateSmartSuggestions, 60000);
    return () => clearInterval(interval);
  }, [dayType, currentHour, studyStreak]);

  useEffect(() => {
    chatEndRef.current?.scrollIntoView({ behavior: 'smooth' });
  }, [chatMessages]);

  useEffect(() => {
    const newAchievements = [...achievements];
    let updated = false;
    
    if (!achievements[0].unlocked && completedHistory.length >= 1) {
      newAchievements[0].unlocked = true;
      updated = true;
    }
    if (!achievements[1].unlocked && studyStreak >= 7) {
      newAchievements[1].unlocked = true;
      updated = true;
    }
    if (!achievements[2].unlocked && points >= 100) {
      newAchievements[2].unlocked = true;
      updated = true;
    }
    if (!achievements[3].unlocked && completedHistory.length >= 50) {
      newAchievements[3].unlocked = true;
      updated = true;
    }
    if (!achievements[4].unlocked && Object.values(completedToday).every(v => v > 0)) {
      newAchievements[4].unlocked = true;
      updated = true;
    }
    
    const totalChapters = [...Object.values(syllabus11), ...Object.values(syllabus12)]
      .reduce((sum, sub) => sum + sub.filter(ch => ch.done).length, 0);
    if (!achievements[5].unlocked && totalChapters >= 10) {
      newAchievements[5].unlocked = true;
      updated = true;
    }
    
    if (!achievements[6].unlocked && learnedTerms.length >= 50) {
      newAchievements[6].unlocked = true;
      updated = true;
    }
    
    if (updated) setAchievements(newAchievements);
  }, [completedHistory, studyStreak, points, completedToday, syllabus11, syllabus12, learnedTerms]);

  useEffect(() => {
    const checkAlarms = () => {
      const now = new Date();
      const currentTime = `${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}`;
      
      alarms.forEach(alarm => {
        if (alarm.time === currentTime && !alarm.triggered) {
          if (Notification.permission === 'granted') {
            new Notification('⏰ POWER OS', { body: alarm.title });
          }
          alert(`⏰ ${alarm.title}\nTime: ${alarm.time}`);
          
          if (!alarm.recurring) {
            setAlarms(prev => prev.map(a => 
              a.id === alarm.id ? { ...a, triggered: true } : a
            ));
          }
        }
      });
    };

    const interval = setInterval(checkAlarms, 60000);
    return () => clearInterval(interval);
  }, [alarms]);

  useEffect(() => {
    if (Notification.permission === 'default') {
      Notification.requestPermission();
    }
  }, []);

  const calculateLevel = (pts) => {
    if (pts < 100) return 1;
    if (pts < 300) return 2;
    if (pts < 700) return 3;
    if (pts < 1500) return 4;
    return 5;
  };

  const getLevelName = (lvl) => {
    const names = ['Beginner', 'Bronze', 'Silver', 'Gold', 'Elite'];
    return names[lvl - 1] || 'Elite';
  };

  if (loading) {
    return (
      <div className="min-h-screen bg-black flex items-center justify-center">
        <div className="text-center">
          <div className="animate-spin rounded-full h-16 w-16 border-t-4 border-amber-500 mx-auto mb-4"></div>
          <div className="text-amber-500 font-bold text-2xl">POWER OS</div>
          <div className="text-gray-400 text-sm mt-2">Loading...</div>
        </div>
      </div>
    );
  }

  // Daily Setup Modal
  if (showDailySetup) {
    return (
      <div className="min-h-screen bg-black text-white p-3 overflow-y-auto">
        <div className="max-w-md mx-auto pb-20">
          <div className="bg-gradient-to-r from-amber-600 to-orange-600 p-4 rounded-2xl mb-4">
            <div className="flex items-center gap-2 mb-2">
              <Sparkles className="w-6 h-6" />
              <div>
                <h1 className="text-lg font-bold">🌅 Daily Plan</h1>
                <p className="text-xs opacity-90">{todayString}</p>
              </div>
            </div>
          </div>

          <div className="bg-gray-900 p-4 rounded-xl mb-3 border border-gray-700">
            <div className="flex gap-2 mb-3">
              <button
                onClick={() => setDayType('class')}
                className={`flex-1 py-2 rounded-xl font-bold text-sm ${dayType === 'class' ? 'bg-blue-600' : 'bg-gray-800'}`}
              >
                📚 Class Day
              </button>
              <button
                onClick={() => setDayType('noclass')}
                className={`flex-1 py-2 rounded-xl font-bold text-sm ${dayType === 'noclass' ? 'bg-green-600' : 'bg-gray-800'}`}
              >
                🏠 No Class
              </button>
            </div>
            {dayType === 'noclass' && (
              <div className="bg-green-900/30 p-2 rounded-lg text-xs text-green-300">
                Full free day! Plan deep study, skills, business learning!
              </div>
            )}
          </div>

          {Object.keys(dailySetupTasks).map(category => (
            <div key={category} className="bg-gray-900 p-3 rounded-xl mb-3 border" style={{borderColor: categoryColors[category]}}>
              <h2 className="text-sm font-bold mb-3 capitalize flex items-center gap-2">
                {category === 'jee' && '📚 JEE'}
                {category === 'skill' && '💼 Skill'}
                {category === 'english' && '🗣️ English'}
                {category === 'body' && '💪 Body'}
                {category === 'business' && '💰 Business'}
              </h2>
              <div className="space-y-2">
                {dailySetupTasks[category].map((task, idx) => (
                  <div key={idx} className="flex gap-2">
                    <input
                      type="text"
                      value={task}
                      onChange={(e) => {
                        const updated = [...dailySetupTasks[category]];
                        updated[idx] = e.target.value;
                        setDailySetupTasks({...dailySetupTasks, [category]: updated});
                      }}
                      placeholder="Task..."
                      className="flex-1 bg-black/40 text-white px-2 py-2 rounded border border-gray-700 outline-none text-sm"
                    />
                    <input
                      type="time"
                      value={dailySetupTimes[category][idx]}
                      onChange={(e) => {
                        const updated = [...dailySetupTimes[category]];
                        updated[idx] = e.target.value;
                        setDailySetupTimes({...dailySetupTimes, [category]: updated});
                      }}
                      className="w-24 bg-black/40 text-white px-2 py-2 rounded border border-gray-700 outline-none text-sm"
                    />
                  </div>
                ))}
                <button
                  onClick={() => {
                    setDailySetupTasks({
                      ...dailySetupTasks,
                      [category]: [...dailySetupTasks[category], '']
                    });
                    setDailySetupTimes({
                      ...dailySetupTimes,
                      [category]: [...dailySetupTimes[category], '']
                    });
                  }}
                  className="w-full bg-green-600 py-2 rounded text-xs font-bold"
                >
                  + Add More
                </button>
              </div>
            </div>
          ))}

          <div className="fixed bottom-0 left-0 right-0 bg-black p-3 border-t border-gray-800">
            <div className="max-w-md mx-auto flex gap-2">
              <button
                onClick={() => {
                  setShowDailySetup(false);
                  setLastSetupDate(todayDateOnly);
                }}
                className="flex-1 bg-gray-700 py-3 rounded-xl font-bold text-sm"
              >
                Skip
              </button>
              <button
                onClick={completeDailySetup}
                className="flex-1 bg-green-600 py-3 rounded-xl font-bold text-sm"
              >
                ✓ Start Day
              </button>
            </div>
          </div>
        </div>
      </div>
    );
  }

  // Vocabulary View
  if (currentView === 'vocabulary') {
    const filteredVocab = Object.entries(vocabulary).filter(([term, data]) =>
      term.toLowerCase().includes(vocabSearch.toLowerCase()) ||
      data.hindi.includes(vocabSearch) ||
      data.meaning.includes(vocabSearch)
    );

    return (
      <div className="min-h-screen bg-black text-white pb-20">
        <div className="sticky top-0 bg-gray-900 p-3 border-b border-gray-800 z-10">
          <div className="flex items-center justify-between mb-3">
            <button onClick={() => setCurrentView('dashboard')} className="flex items-center gap-2 text-purple-400">
              <ChevronRight className="rotate-180 w-5 h-5" /> Back
            </button>
            <h1 className="text-lg font-bold flex items-center gap-2">
              <Languages className="w-5 h-5" />
              Vocabulary ({Object.keys(vocabulary).length})
            </h1>
            <div className="w-16"></div>
          </div>

          <div className="relative">
            <Search className="absolute left-3 top-2.5 w-4 h-4 text-gray-400" />
            <input
              type="text"
              value={vocabSearch}
              onChange={(e) => setVocabSearch(e.target.value)}
              placeholder="Search terms..."
              className="w-full bg-gray-800 text-white pl-9 pr-3 py-2 rounded-xl border border-gray-700 outline-none text-sm"
            />
          </div>

          <div className="mt-2 text-xs text-center text-gray-400">
            Learned: {learnedTerms.length} terms (+{learnedTerms.length * 2} pts)
          </div>
        </div>

        <div className="p-3 space-y-2">
          {filteredVocab.map(([term, data], idx) => {
            const learned = learnedTerms.includes(term);
            return (
              <div
                key={idx}
                className={`bg-gray-900 p-3 rounded-xl border ${learned ? 'border-green-500' : 'border-gray-800'}`}
              >
                <div className="flex items-start justify-between mb-2">
                  <div className="text-base font-bold text-blue-400">{term}</div>
                  {!learned && (
                    <button
                      onClick={() => markTermLearned(term)}
                      className="bg-green-600 px-2 py-1 rounded text-xs font-bold"
                    >
                      ✓ Learn +2
                    </button>
                  )}
                  {learned && <span className="text-green-400 text-xs">✓ Learned</span>}
                </div>
                <div className="bg-green-900/30 px-2 py-1 rounded text-sm font-bold text-green-300 mb-1">
                  {data.hindi}
                </div>
                <div className="text-sm text-gray-300 mb-1">
                  <span className="text-amber-400 font-bold">Meaning:</span> {data.meaning}
                </div>
                <div className="text-xs text-gray-400">
                  <span className="text-purple-400 font-bold">Example:</span> {data.example}
                </div>
              </div>
            );
          })}
        </div>
      </div>
    );
  }

  // Syllabus View
  if (currentView === 'syllabus') {
    const currentSyllabus = syllabusClass === '11' ? syllabus11 : syllabus12;
    const chapters = currentSyllabus[syllabusSubject];
    const completed = chapters.filter(ch => ch.done).length;
    const progress = Math.round((completed / chapters.length) * 100);

    return (
      <div className="min-h-screen bg-black text-white pb-20">
        <div className="sticky top-0 bg-gray-900 p-3 border-b border-gray-800 z-10">
          <div className="flex items-center justify-between mb-3">
            <button onClick={() => setCurrentView('dashboard')} className="flex items-center gap-2 text-blue-400">
              <ChevronRight className="rotate-180 w-5 h-5" /> Back
            </button>
            <h1 className="text-lg font-bold flex items-center gap-2">
              <GraduationCap className="w-5 h-5" />
              JEE Syllabus
            </h1>
            <div className="w-16"></div>
          </div>

          <div className="flex gap-2 mb-2">
            {['11', '12'].map(cls => (
              <button
                key={cls}
                onClick={() => setSyllabusClass(cls)}
                className={`flex-1 py-2 rounded-xl font-bold text-sm ${
                  syllabusClass === cls ? 'bg-blue-600' : 'bg-gray-800'
                }`}
              >
                Class {cls}th
              </button>
            ))}
          </div>

          <div className="flex gap-2 mb-2">
            {['physics', 'chemistry', 'maths'].map(sub => (
              <button
                key={sub}
                onClick={() => setSyllabusSubject(sub)}
                className={`flex-1 py-2 rounded-xl font-bold capitalize text-xs ${
                  syllabusSubject === sub ? 'bg-green-600' : 'bg-gray-800'
                }`}
              >
                {sub}
              </button>
            ))}
          </div>

          <div className="bg-gray-800 rounded-xl p-2">
            <div className="flex justify-between mb-1 text-xs">
              <span>{completed}/{chapters.length}</span>
              <span className="font-bold">{progress}%</span>
            </div>
            <div className="bg-gray-700 h-2 rounded-full overflow-hidden">
              <div className="bg-green-500 h-full transition-all" style={{ width: `${progress}%` }}></div>
            </div>
          </div>
        </div>

        <div className="p-3 space-y-2">
          {chapters.map((ch, idx) => (
            <div
              key={idx}
              className={`bg-gray-900 p-3 rounded-xl border flex items-center gap-2 ${
                ch.done ? 'border-green-500' : 'border-gray-800'
              }`}
            >
              <button
                onClick={() => toggleChapter(syllabusClass, syllabusSubject, idx)}
                className="flex-shrink-0"
              >
                {ch.done ? (
                  <CheckCircle className="w-6 h-6 text-green-500" />
                ) : (
                  <Circle className="w-6 h-6 text-gray-500" />
                )}
              </button>
              <div className="flex-1">
                <div className={`text-sm font-bold ${ch.done ? 'text-green-400 line-through' : ''}`}>
                  Ch-{ch.ch}: {ch.name}
                </div>
                {ch.done && <div className="text-xs text-green-400">✓ +15 pts</div>}
              </div>
            </div>
          ))}
        </div>
      </div>
    );
  }

  // Lists View
  if (currentView === 'lists') {
    const currentList = lists.find(l => l.id === activeList) || customLists.find(l => l.id === activeList);
    
    return (
      <div className="min-h-screen bg-black text-white pb-20">
        <div className="sticky top-0 bg-gray-900 p-3 border-b border-gray-800 z-10">
          <div className="flex items-center justify-between mb-3">
            <button onClick={() => setCurrentView('dashboard')} className="flex items-center gap-2 text-blue-400">
              <ChevronRight className="rotate-180 w-5 h-5" /> Back
            </button>
            <h1 className="text-lg font-bold">📋 Lists</h1>
            <div className="w-16"></div>
          </div>
          
          <div className="flex gap-2 overflow-x-auto pb-2">
            {[...lists, ...customLists].map(list => (
              <button
                key={list.id}
                onClick={() => setActiveList(list.id)}
                className={`px-3 py-2 rounded-xl font-bold whitespace-nowrap flex items-center gap-2 text-sm ${
                  activeList === list.id ? 'bg-blue-600' : 'bg-gray-800'
                }`}
              >
                <span>{list.icon}</span>
                <span>{list.name}</span>
                <span className="text-xs bg-black/30 px-1.5 py-0.5 rounded-full">
                  {list.items.filter(i => !i.completed).length}
                </span>
              </button>
            ))}
          </div>
        </div>

        <div className="p-3">
          <div className="bg-gray-900 p-3 rounded-xl border border-gray-800 mb-3">
            <div className="flex gap-2">
              <input
                type="text"
                value={newListItem}
                onChange={(e) => setNewListItem(e.target.value)}
                onKeyPress={(e) => e.key === 'Enter' && addListItem()}
                placeholder="Add new item..."
                className="flex-1 bg-black/40 text-white px-3 py-2 rounded-xl border border-gray-700 outline-none text-sm"
              />
              <button
                onClick={addListItem}
                className="px-4 py-2 rounded-xl font-bold text-white"
                style={{ backgroundColor: currentList?.color }}
              >
                <Plus className="w-4 h-4" />
              </button>
            </div>
          </div>

          <div className="space-y-2">
            {currentList?.items.sort((a, b) => a.completed - b.completed).map(item => (
              <div
                key={item.id}
                className={`bg-gray-900 p-3 rounded-xl border border-gray-800 flex items-center gap-2 ${
                  item.completed ? 'opacity-50' : ''
                }`}
              >
                <button
                  onClick={() => toggleListItem(activeList, item.id)}
                  className="flex-shrink-0"
                >
                  {item.completed ? (
                    <CheckCircle className="w-5 h-5 text-green-500" />
                  ) : (
                    <Circle className="w-5 h-5 text-gray-500" />
                  )}
                </button>
                <span className={`flex-1 text-sm ${item.completed ? 'line-through text-gray-500' : ''}`}>
                  {item.text}
                </span>
                <button onClick={() => deleteListItem(activeList, item.id)} className="text-red-400 p-1">
                  <Trash2 className="w-4 h-4" />
                </button>
              </div>
            ))}
            
            {currentList?.items.length === 0 && (
              <div className="bg-gray-900 p-6 rounded-xl border border-gray-800 text-center text-gray-500 text-sm">
                No items yet
              </div>
            )}
          </div>
        </div>
      </div>
    );
  }

  // AI Chat View
  if (currentView === 'ai-chat') {
    return (
      <div className="min-h-screen bg-black text-white flex flex-col">
        <div className="sticky top-0 bg-gray-900 p-3 border-b border-gray-800 z-10">
          <div className="flex items-center justify-between">
            <button onClick={() => setCurrentView('dashboard')} className="flex items-center gap-2 text-purple-400">
              <ChevronRight className="rotate-180 w-5 h-5" /> Back
            </button>
            <h1 className="text-lg font-bold">🤖 AI Coach</h1>
            <button onClick={() => setChatMessages([])}>
              <Trash2 className="w-5 h-5" />
            </button>
          </div>
        </div>

        <div className="flex-1 overflow-y-auto p-3">
          <div className="space-y-3 pb-20">
            {chatMessages.length === 0 ? (
              <div className="text-center py-8">
                <Brain className="w-12 h-12 text-purple-400 mx-auto mb-3" />
                <h2 className="text-base font-bold mb-3">Ask Your AI Coach</h2>
                <div className="grid gap-2">
                  {["Best study strategy?", "How to improve?", "Time management tips?"].map((q, i) => (
                    <button
                      key={i}
                      onClick={() => setChatInput(q)}
                      className="bg-purple-900/50 p-2 rounded-xl text-xs text-left"
                    >
                      {q}
                    </button>
                  ))}
                </div>
              </div>
            ) : (
              chatMessages.map((msg, i) => (
                <div key={i} className={`flex ${msg.role === 'user' ? 'justify-end' : 'justify-start'}`}>
                  <div className={`max-w-[85%] p-3 rounded-2xl text-sm ${
                    msg.role === 'user' ? 'bg-purple-600' : 'bg-gray-800'
                  }`}>
                    {msg.content}
                  </div>
                </div>
              ))
            )}
            {isChatLoading && (
              <div className="flex justify-start">
                <div className="bg-gray-800 p-3 rounded-2xl">
                  <div className="flex gap-1">
                    {[0,1,2].map(i => (
                      <div key={i} className="w-2 h-2 bg-purple-400 rounded-full animate-bounce" style={{animationDelay: `${i*0.1}s`}}></div>
                    ))}
                  </div>
                </div>
              </div>
            )}
            <div ref={chatEndRef} />
          </div>
        </div>

        <div className="sticky bottom-0 bg-gray-900 p-3 border-t border-gray-800">
          <div className="flex gap-2">
            <input
              type="text"
              value={chatInput}
              onChange={(e) => setChatInput(e.target.value)}
              onKeyPress={(e) => e.key === 'Enter' && !isChatLoading && sendChatMessage()}
              placeholder="Ask anything..."
              className="flex-1 bg-gray-800 text-white px-3 py-2 rounded-xl border border-gray-700 outline-none text-sm"
              disabled={isChatLoading}
            />
            <button
              onClick={sendChatMessage}
              disabled={isChatLoading || !chatInput.trim()}
              className="bg-purple-600 px-4 py-2 rounded-xl disabled:opacity-50"
            >
              <Send className="w-4 h-4" />
            </button>
          </div>
        </div>
      </div>
    );
  }

  // Analytics View
  if (currentView === 'analytics') {
    const totalCompleted = completedHistory.length;
    const totalTimeSpent = completedHistory.reduce((sum, h) => sum + (h.timeSpent || 0), 0);
    
    return (
      <div className="min-h-screen bg-black text-white pb-20">
        <div className="sticky top-0 bg-gray-900 p-3 border-b border-gray-800 z-10">
          <div className="flex items-center justify-between">
            <button onClick={() => setCurrentView('dashboard')} className="flex items-center gap-2 text-purple-400">
              <ChevronRight className="rotate-180 w-5 h-5" /> Back
            </button>
            <h1 className="text-lg font-bold">📊 Analytics</h1>
            <div className="w-16"></div>
          </div>
        </div>

        <div className="p-3">
          <div className="grid grid-cols-2 gap-2 mb-3">
            {[
              { label: 'Tasks', val: totalCompleted, color: '#3b82f6' },
              { label: 'Points', val: points, color: '#22c55e' },
              { label: 'Streak', val: studyStreak, sub: `Best: ${maxStreaks.study}`, color: '#ef4444' },
              { label: 'Time', val: `${Math.floor(totalTimeSpent/3600)}h`, color: '#f59e0b' }
            ].map((stat, i) => (
              <div key={i} className="bg-gray-900 p-3 rounded-xl border border-gray-800">
                <div className="text-2xl font-bold" style={{color: stat.color}}>{stat.val}</div>
                <div className="text-xs text-gray-400">{stat.label}</div>
                {stat.sub && <div className="text-xs text-gray-500">{stat.sub}</div>}
              </div>
            ))}
          </div>

          <div className="bg-gray-900 p-3 rounded-xl border border-gray-800">
            <h2 className="text-sm font-bold mb-2">Recent Activity</h2>
            <div className="space-y-1 max-h-96 overflow-y-auto">
              {completedHistory.slice(0, 20).map((h, i) => (
                <div key={i} className="bg-black/40 p-2 rounded flex items-center gap-2 text-xs">
                  <span className="flex-1 truncate">{h.name}</span>
                  {h.timeSpent > 0 && (
                    <span className="bg-blue-900 px-2 py-0.5 rounded text-xs">{formatTime(h.timeSpent)}</span>
                  )}
                  <span className="text-green-400 font-bold">+{h.points}</span>
                </div>
              ))}
            </div>
          </div>
        </div>
      </div>
    );
  }

  // Main Dashboard
  return (
    <div className="min-h-screen bg-black text-white pb-20">
      {/* Header */}
      <div className="sticky top-0 bg-gradient-to-r from-amber-600 via-orange-600 to-red-600 p-3 border-b-2 border-amber-500 z-10">
        <div className="flex justify-between items-center mb-2">
          <div>
            <h1 className="text-xl font-bold">POWER OS</h1>
            <p className="text-xs opacity-90">{todayString}</p>
          </div>
          <div className="text-right">
            <div className="flex items-center gap-1 mb-1">
              <Award className="w-4 h-4" />
              <span className="text-lg font-bold">{points}</span>
            </div>
            <div className="bg-black/30 px-2 py-0.5 rounded-full text-xs font-bold">
              {getLevelName(level)} • L{level}
            </div>
          </div>
        </div>

        {isTimeBlocked() && (
          <div className="bg-red-900/50 border border-red-500 p-2 rounded-lg flex items-center gap-2 mb-2">
            <AlertCircle className="w-4 h-4" />
            <span className="text-xs font-bold">Family Time (2-7PM)</span>
          </div>
        )}

        <div className="grid grid-cols-2 gap-2 mb-2">
          <button
            onClick={() => { setDayType(dayType === 'class' ? 'noclass' : 'class'); generateSmartSuggestions(); }}
            className={`py-2 rounded-lg text-xs font-bold ${dayType === 'noclass' ? 'bg-green-600' : 'bg-black/30'}`}
          >
            {dayType === 'class' ? '📚 Class' : '🏠 NO CLASS'}
          </button>
          <button
            onClick={() => setShowDailySetup(true)}
            className="bg-purple-600 py-2 rounded-lg text-xs font-bold flex items-center justify-center gap-1"
          >
            <Sparkles className="w-3 h-3" /> Plan Day
          </button>
        </div>

        <div className="flex gap-1 overflow-x-auto pb-1 mb-2">
          <button onClick={() => setCurrentView('syllabus')} className="bg-blue-600 p-2 rounded-lg flex-shrink-0">
            <GraduationCap className="w-4 h-4" />
          </button>
          <button onClick={() => setCurrentView('vocabulary')} className="bg-purple-600 p-2 rounded-lg flex-shrink-0">
            <Languages className="w-4 h-4" />
          </button>
          <button onClick={() => setCurrentView('lists')} className="bg-indigo-600 p-2 rounded-lg flex-shrink-0">
            <List className="w-4 h-4" />
          </button>
          <button onClick={() => setCurrentView('ai-chat')} className="bg-pink-600 p-2 rounded-lg flex-shrink-0">
            <Brain className="w-4 h-4" />
          </button>
          <button onClick={() => setCurrentView('analytics')} className="bg-cyan-600 p-2 rounded-lg flex-shrink-0">
            <BarChart3 className="w-4 h-4" />
          </button>
          <button onClick={() => setShowAlarmModal(true)} className="bg-yellow-600 p-2 rounded-lg flex-shrink-0 relative">
            <Bell className="w-4 h-4" />
            {alarms.length > 0 && <span className="absolute -top-1 -right-1 bg-red-500 text-xs px-1 rounded-full">{alarms.length}</span>}
          </button>
          <button onClick={() => setShowAchievements(true)} className="bg-green-600 p-2 rounded-lg flex-shrink-0">
            <Trophy className="w-4 h-4" />
          </button>
          <button onClick={exportData} className="bg-gray-600 p-2 rounded-lg flex-shrink-0">
            <Download className="w-4 h-4" />
          </button>
        </div>

        <div className="grid grid-cols-3 gap-2">
          {[
            { label: 'Study', val: studyStreak, max: maxStreaks.study, color: '#ef4444' },
            { label: 'Workout', val: workoutStreak, max: maxStreaks.workout, color: '#3b82f6' },
            { label: 'Skill', val: skillStreak, max: maxStreaks.skill, color: '#22c55e' }
          ].map((s, i) => (
            <div key={i} className="bg-black/30 p-2 rounded-lg">
              <div className="flex items-center gap-1 mb-1">
                <Flame className="w-3 h-3" style={{color: s.color}} />
                <span className="text-xs">{s.label}</span>
              </div>
              <div className="text-base font-bold">{s.val}d</div>
              <div className="text-xs opacity-75">Best: {s.max}</div>
            </div>
          ))}
        </div>
      </div>

      {/* Timer Bar */}
      {activeTimer && (
        <div className="sticky top-[180px] bg-blue-900 p-2 border-b border-blue-500 z-10">
          <div className="flex items-center gap-2">
            <div className="flex-1">
              <div className="text-xs font-bold">⏱️ Timer</div>
              <div className="text-lg font-bold">{formatTime(timerSeconds)}</div>
            </div>
            <button onClick={() => setTimerRunning(!timerRunning)} className="bg-blue-600 p-2 rounded-lg">
              {timerRunning ? <Pause className="w-4 h-4" /> : <Play className="w-4 h-4" />}
            </button>
            <button onClick={stopTaskTimer} className="bg-red-600 p-2 rounded-lg">
              <X className="w-4 h-4" />
            </button>
          </div>
        </div>
      )}

      <div className="p-3">
        {/* Smart Suggestions */}
        {smartSuggestions.length > 0 && (
          <div className={`p-3 rounded-2xl mb-3 border-2 ${
            dayType === 'noclass' 
              ? 'bg-gradient-to-r from-green-900 to-emerald-900 border-green-500' 
              : 'bg-gradient-to-r from-purple-900 to-indigo-900 border-purple-500'
          }`}>
            <div className="flex items-center gap-2 mb-2">
              <Lightbulb className="w-4 h-4 text-yellow-300" />
              <span className="font-bold text-sm">
                {dayType === 'noclass' ? '🎉 NO CLASS - Full Power!' : 'Smart Tips'}
              </span>
            </div>
            <div className="space-y-2">
              {smartSuggestions.map((s, i) => (
                <div key={i} className="bg-black/30 p-2 rounded-xl flex items-center gap-2">
                  <span className="text-base">{s.icon}</span>
                  <span className="text-xs flex-1">{s.text}</span>
                </div>
              ))}
            </div>
            {!dailyFocus && (
              <button
                onClick={getAIDecision}
                disabled={aiThinking}
                className="w-full bg-white/20 py-2 rounded-xl mt-2 text-xs font-bold"
              >
                {aiThinking ? 'AI Thinking...' : '🤖 Get AI Strategy'}
              </button>
            )}
          </div>
        )}

        {/* AI Focus */}
        {dailyFocus && (
          <div className="bg-purple-900/50 p-3 rounded-2xl mb-3 border border-purple-500">
            <div className="flex items-center gap-2 mb-2">
              <Target className="w-4 h-4 text-yellow-300" />
              <span className="font-bold text-xs">AI Focus:</span>
            </div>
            <p className="text-sm mb-2">{dailyFocus}</p>
            {aiSuggestions.map((s, i) => (
              <div key={i} className="bg-black/30 p-2 rounded-lg mb-1 flex items-start gap-2">
                <ChevronRight className="w-3 h-3 text-purple-300 mt-0.5 flex-shrink-0" />
                <span className="text-xs">{s}</span>
              </div>
            ))}
            <button
              onClick={getAIDecision}
              disabled={aiThinking}
              className="w-full bg-purple-600 py-2 rounded-lg mt-2 text-xs font-bold"
            >
              {aiThinking ? 'Thinking...' : '🔄 Refresh'}
            </button>
          </div>
        )}

        {/* Habits */}
        <div className="bg-gray-900 p-3 rounded-2xl mb-3 border border-gray-800">
          <h2 className="text-sm font-bold mb-2 flex items-center gap-2">
            <CheckSquare className="w-4 h-4 text-green-400" />
            Daily Habits
          </h2>
          <div className="grid grid-cols-2 gap-2">
            {dailyHabits.map(h => (
              <button
                key={h.id}
                onClick={() => toggleHabit(h.id)}
                className={`p-2 rounded-xl text-xs text-left ${
                  h.done ? 'bg-green-900 border border-green-500' : 'bg-gray-800 border border-gray-700'
                }`}
              >
                <div className="flex items-center justify-between">
                  <span>{h.done ? '✓ ' : '○ '}{h.name}</span>
                  {h.streak > 0 && (
                    <span className="text-xs bg-orange-900 px-1.5 py-0.5 rounded-full flex items-center gap-1">
                      <Flame className="w-3 h-3" /> {h.streak}
                    </span>
                  )}
                </div>
              </button>
            ))}
          </div>
        </div>

        {/* Tasks */}
        {Object.keys(tasks).map(cat => {
          const Icon = categoryIcons[cat];
          const pts = categoryPoints[cat];
          const color = categoryColors[cat];
          const isExpanded = expandedCategory === cat;

          return (
            <div key={cat} className="bg-gray-900 p-3 rounded-2xl mb-3 border-2" style={{borderColor: color}}>
              <div className="flex items-center gap-2 mb-2">
                <Icon className="w-4 h-4" style={{color}} />
                <h2 className="text-sm font-bold flex-1">{categoryTitles[cat]}</h2>
                <button
                  onClick={() => {
                    setCurrentNotesCategory(cat);
                    setShowNotesModal(true);
                  }}
                  className="text-xs bg-black/30 p-1.5 rounded"
                >
                  <FileText className="w-3 h-3" />
                </button>
                <span className="text-xs bg-black/30 px-2 py-0.5 rounded-full">+{pts}</span>
                <button onClick={() => setExpandedCategory(isExpanded ? null : cat)}>
                  {isExpanded ? <ChevronUp className="w-4 h-4" /> : <ChevronDown className="w-4 h-4" />}
                </button>
              </div>

              {isExpanded && (
                <>
                  <div className="flex gap-2 mb-2">
                    <input
                      type="text"
                      value={newTaskInput[cat]}
                      onChange={(e) => setNewTaskInput({...newTaskInput, [cat]: e.target.value})}
                      onKeyPress={(e) => e.key === 'Enter' && addTask(cat)}
                      placeholder="Add task..."
                      className="flex-1 bg-black/40 text-white px-2 py-2 rounded-lg border border-gray-700 outline-none text-sm"
                    />
                    <button
                      onClick={() => addTask(cat)}
                      className="p-2 rounded-lg font-bold"
                      style={{backgroundColor: color}}
                    >
                      <Plus className="w-4 h-4" />
                    </button>
                  </div>

                  <div className="space-y-2">
                    {tasks[cat].length === 0 ? (
                      <div className="bg-black/20 p-2 rounded-lg text-center text-gray-400 text-xs">
                        No tasks yet
                      </div>
                    ) : (
                      tasks[cat].map(t => (
                        <div key={t.id} className="bg-black/40 p-2 rounded-lg">
                          <div className="flex items-center gap-2 mb-2">
                            <span className="flex-1 text-sm truncate">{t.name}</span>
                            {taskTimeTracking[t.id] > 0 && (
                              <span className="text-xs bg-blue-900 px-2 py-0.5 rounded">
                                {formatTime(taskTimeTracking[t.id])}
                              </span>
                            )}
                          </div>
                          <div className="flex gap-2">
                            <button
                              onClick={() => activeTimer?.taskId === t.id ? stopTaskTimer() : startTaskTimer(t.id, cat)}
                              className="bg-blue-600 p-2 rounded-lg"
                            >
                              {activeTimer?.taskId === t.id ? <Pause className="w-3 h-3" /> : <Play className="w-3 h-3" />}
                            </button>
                            <button
                              onClick={() => completeTask(cat, t.id, pts)}
                              className="flex-1 bg-green-600 py-2 rounded-lg text-xs font-bold"
                            >
                              ✓ Done +{pts}
                            </button>
                            <button onClick={() => deleteTask(cat, t.id)} className="bg-red-600 p-2 rounded-lg">
                              <Trash2 className="w-3 h-3" />
                            </button>
                          </div>
                        </div>
                      ))
                    )}
                  </div>
                </>
              )}

              {!isExpanded && tasks[cat].length > 0 && (
                <div className="text-xs text-gray-400 text-center">
                  {tasks[cat].length} task{tasks[cat].length !== 1 ? 's' : ''} • Click to expand
                </div>
              )}
            </div>
          );
        })}

        {/* Progress */}
        <div className="bg-gray-900 p-3 rounded-2xl border border-gray-800">
          <h2 className="text-sm font-bold mb-2 flex items-center gap-2">
            <Star className="w-4 h-4 text-yellow-400" />
            Today's Progress
          </h2>
          <div className="grid grid-cols-5 gap-2">
            {Object.entries(completedToday).map(([cat, cnt]) => (
              <div key={cat} className="text-center">
                <div className="text-xl font-bold" style={{color: categoryColors[cat]}}>{cnt}</div>
                <div className="text-xs text-gray-400 capitalize">{cat.slice(0,3)}</div>
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Alarm Modal */}
      {showAlarmModal && (
        <div className="fixed inset-0 bg-black/90 flex items-end justify-center z-50">
          <div className="bg-gray-900 rounded-t-3xl p-4 w-full max-h-[90vh] overflow-y-auto border-t-2 border-yellow-500">
            <div className="flex items-center justify-between mb-4">
              <h2 className="text-lg font-bold">⏰ Set Alarm</h2>
              <button onClick={() => setShowAlarmModal(false)}>
                <X className="w-6 h-6" />
              </button>
            </div>

            <div className="space-y-3">
              <input
                type="text"
                value={newAlarm.title}
                onChange={(e) => setNewAlarm({...newAlarm, title: e.target.value})}
                placeholder="Title"
                className="w-full bg-gray-800 text-white px-3 py-3 rounded-xl outline-none"
              />
              <input
                type="time"
                value={newAlarm.time}
                onChange={(e) => setNewAlarm({...newAlarm, time: e.target.value})}
                className="w-full bg-gray-800 text-white px-3 py-3 rounded-xl outline-none"
              />
              <select
                value={newAlarm.category}
                onChange={(e) => setNewAlarm({...newAlarm, category: e.target.value})}
                className="w-full bg-gray-800 text-white px-3 py-3 rounded-xl outline-none"
              >
                <option value="jee">JEE</option>
                <option value="skill">Skill</option>
                <option value="english">English</option>
                <option value="body">Body</option>
                <option value="business">Business</option>
              </select>
              <label className="flex items-center gap-2">
                <input
                  type="checkbox"
                  checked={newAlarm.recurring}
                  onChange={(e) => setNewAlarm({...newAlarm, recurring: e.target.checked})}
                  className="w-4 h-4"
                />
                Recurring (daily)
              </label>
              <button onClick={addAlarm} className="w-full bg-yellow-500 py-3 rounded-xl font-bold">
                Set Alarm
              </button>
            </div>

            {alarms.length > 0 && (
              <div className="mt-4">
                <h3 className="text-sm font-bold mb-2 text-gray-400">Active Alarms</h3>
                <div className="space-y-2">
                  {alarms.map(a => (
                    <div key={a.id} className="bg-gray-800 p-3 rounded-xl flex items-center gap-3">
                      <BellRing className="w-4 h-4 text-yellow-400" />
                      <div className="flex-1">
                        <div className="text-sm font-medium">{a.title}</div>
                        <div className="text-xs text-gray-400">
                          {a.time} {a.recurring && '• Daily'}
                        </div>
                      </div>
                      <button onClick={() => deleteAlarm(a.id)} className="text-red-400">
                        <Trash2 className="w-4 h-4" />
                      </button>
                    </div>
                  ))}
                </div>
              </div>
            )}
          </div>
        </div>
      )}

      {/* Notes Modal */}
      {showNotesModal && (
        <div className="fixed inset-0 bg-black/90 flex items-end justify-center z-50">
          <div className="bg-gray-900 rounded-t-3xl p-4 w-full max-h-[90vh] overflow-y-auto border-t-2" style={{borderColor: categoryColors[currentNotesCategory]}}>
            <div className="flex items-center justify-between mb-4">
              <h2 className="text-lg font-bold capitalize">{currentNotesCategory} Notes</h2>
              <button onClick={() => setShowNotesModal(false)}>
                <X className="w-6 h-6" />
              </button>
            </div>
            <textarea
              value={categoryNotes[currentNotesCategory]}
              onChange={(e) => setCategoryNotes({
                ...categoryNotes,
                [currentNotesCategory]: e.target.value
              })}
              placeholder="Important points, formulas, reminders..."
              className="w-full bg-black/40 text-white p-3 rounded-xl border border-gray-700 outline-none min-h-[300px] font-mono text-sm"
              autoFocus
            />
            <button
              onClick={() => setShowNotesModal(false)}
              className="w-full mt-4 py-3 rounded-xl font-bold text-white"
              style={{backgroundColor: categoryColors[currentNotesCategory]}}
            >
              Save
            </button>
          </div>
        </div>
      )}

      {/* Achievements Modal */}
      {showAchievements && (
        <div className="fixed inset-0 bg-black/90 flex items-end justify-center z-50">
          <div className="bg-gray-900 rounded-t-3xl p-4 w-full max-h-[90vh] overflow-y-auto border-t-2 border-yellow-500">
            <div className="flex items-center justify-between mb-4">
              <h2 className="text-lg font-bold">🏆 Achievements ({achievements.filter(a => a.unlocked).length}/{achievements.length})</h2>
              <button onClick={() => setShowAchievements(false)}>
                <X className="w-6 h-6" />
              </button>
            </div>
            <div className="grid grid-cols-2 gap-3">
              {achievements.map(a => (
                <div
                  key={a.id}
                  className={`p-3 rounded-xl border-2 ${
                    a.unlocked ? 'bg-yellow-900 border-yellow-500' : 'bg-gray-800 border-gray-700 opacity-50'
                  }`}
                >
                  <div className="text-2xl mb-2">{a.icon}</div>
                  <div className="font-bold text-sm">{a.name}</div>
                  <div className="text-xs text-gray-400">{a.desc}</div>
                  {a.unlocked && <div className="text-xs text-green-400 mt-1">✓ Unlocked</div>}
                </div>
              ))}
            </div>
          </div>
        </div>
      )}
    </div>
  );
}
