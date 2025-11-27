import React, { useState, useEffect, useMemo } from 'react';
import { 
  Calendar, 
  ChefHat, 
  ShoppingBag, 
  Utensils, 
  RefreshCw, 
  ChevronRight, 
  Clock, 
  Flame, 
  Info,
  Heart,
  X,
  CheckCircle2,
  Salad
} from 'lucide-react';

// --- 数据源 (Mock Data) ---
// 包含丰富的食谱库，确保多样性
const RECIPE_DATABASE = {
  breakfast: [
    { id: 'b1', name: '全麦牛油果煎蛋吐司', calories: 350, tags: ['优质脂肪', '快手'], ingredients: ['全麦面包 2片', '牛油果 半个', '鸡蛋 1个', '黑胡椒 少许'], steps: ['面包烤脆', '牛油果捣泥涂抹', '煎一个太阳蛋铺在上面', '撒上黑胡椒'] },
    { id: 'b2', name: '高蛋白燕麦蓝莓碗', calories: 300, tags: ['高纤维', '抗氧化'], ingredients: ['即食燕麦 50g', '牛奶/杏仁奶 200ml', '蓝莓 1把', '蛋白粉 1勺'], steps: ['燕麦加奶煮熟或微波', '拌入蛋白粉', '撒上新鲜蓝莓和坚果碎'] },
    { id: 'b3', name: '中式杂粮粥配水煮蛋', calories: 280, tags: ['养胃', '低脂'], ingredients: ['黑米/糙米/红豆 50g', '鸡蛋 1个', '小咸菜 少许'], steps: ['杂粮提前浸泡一晚', '电饭煲煮粥模式', '配一个水煮蛋'] },
    { id: 'b4', name: '蔬菜鸡胸肉卷饼', calories: 380, tags: ['高蛋白', '饱腹'], ingredients: ['全麦卷饼皮 1张', '鸡胸肉 50g', '生菜/黄瓜 适量', '低脂沙拉酱'], steps: ['鸡胸肉煎熟切条', '饼皮加热', '卷入蔬菜和鸡肉'] },
    { id: 'b5', name: '香蕉坚果酸奶杯', calories: 320, tags: ['益生菌', '快手'], ingredients: ['希腊酸奶 150g', '香蕉 1根', '混合坚果 20g'], steps: ['杯底铺一层酸奶', '铺一层香蕉片', '再铺酸奶，顶部撒坚果'] },
    { id: 'b6', name: '番茄鸡蛋荞麦面', calories: 400, tags: ['低GI', '家常'], ingredients: ['荞麦面 60g', '番茄 1个', '鸡蛋 1个', '青菜 2颗'], steps: ['番茄炒出汁加水', '放入荞麦面煮熟', '打入蛋花和青菜'] },
    { id: 'b7', name: '蒸紫薯与无糖豆浆', calories: 250, tags: ['粗粮', '植物蛋白'], ingredients: ['紫薯 150g', '黄豆 30g'], steps: ['紫薯蒸熟', '黄豆提前泡发打豆浆'] },
  ],
  lunch: [
    { id: 'l1', name: '香煎三文鱼配藜麦饭', calories: 550, tags: ['Omega-3', '优质主食'], ingredients: ['三文鱼 150g', '藜麦/糙米饭 1碗', '西兰花 100g', '柠檬'], steps: ['三文鱼煎至金黄挤柠檬汁', '西兰花焯水', '搭配藜麦饭装盘'] },
    { id: 'l2', name: '去皮照烧鸡腿饭', calories: 600, tags: ['高蛋白', '开胃'], ingredients: ['鸡腿 1个', '杂粮饭 1碗', '胡萝卜 50g', '照烧汁'], steps: ['鸡腿去骨去皮', '煎至两面金黄倒入照烧汁收汁', '配水煮胡萝卜和米饭'] },
    { id: 'l3', name: '蒜蓉西蓝花炒虾仁', calories: 450, tags: ['低卡', '鲜美'], ingredients: ['虾仁 150g', '西兰花 200g', '蒜末', '魔芋结'], steps: ['虾仁焯水变色', '爆香蒜末炒西兰花', '加入虾仁和调味', '可配少量主食'] },
    { id: 'l4', name: '彩椒牛肉粒意面', calories: 580, tags: ['补铁', '西式'], ingredients: ['牛排肉 100g', '彩椒 半个', '意大利面 60g', '黑胡椒酱'], steps: ['意面煮熟捞出', '牛肉切粒炒熟', '加入彩椒和意面翻炒'] },
    { id: 'l5', name: '口蘑豆腐煲', calories: 420, tags: ['素食', '鲜美'], ingredients: ['嫩豆腐 1块', '口蘑 100g', '青豆', '蚝油'], steps: ['豆腐切块煎黄', '口蘑炒软', '加水炖煮5分钟收汁'] },
    { id: 'l6', name: '清爽越式牛肉河粉', calories: 500, tags: ['清淡', '汤类'], ingredients: ['河粉/米粉 1份', '肥牛卷 100g', '豆芽', '九层塔', '青柠'], steps: ['高汤煮沸', '烫熟河粉和肥牛', '加入豆芽香草挤柠檬汁'] },
    { id: 'l7', name: '金枪鱼玉米沙拉饭团', calories: 480, tags: ['便携', '均衡'], ingredients: ['水浸金枪鱼 1罐', '玉米粒', '米饭', '海苔碎'], steps: ['金枪鱼沥水拌入玉米粒和沙拉酱', '包入米饭捏成饭团'] },
  ],
  dinner: [
    { id: 'd1', name: '冬瓜蛤蜊汤配凉拌菜', calories: 300, tags: ['低脂', '去水肿'], ingredients: ['蛤蜊 200g', '冬瓜 200g', '姜丝', '黄瓜 1根'], steps: ['蛤蜊吐沙', '冬瓜切片煮汤', '出锅前加蛤蜊煮开口', '配凉拌黄瓜'] },
    { id: 'd2', name: '白灼菜心与蒸红薯', calories: 350, tags: ['高纤维', '清肠'], ingredients: ['广东菜心 200g', '红薯 150g', '蒸鱼豉油'], steps: ['红薯蒸熟', '菜心焯水淋上豉油'] },
    { id: 'd3', name: '番茄龙利鱼汤', calories: 380, tags: ['好消化', '酸甜开胃'], ingredients: ['龙利鱼/巴沙鱼 1条', '番茄 2个', '金针菇'], steps: ['番茄炒化加水', '放入金针菇煮沸', '下鱼片煮2分钟'] },
    { id: 'd4', name: '日式关东煮(自制版)', calories: 400, tags: ['暖胃', '低卡'], ingredients: ['白萝卜', '魔芋丝', '海带结', '鱼丸 2-3个', '昆布高汤'], steps: ['昆布煮汤底', '放入不容易熟的萝卜煮软', '加入其他食材'] },
    { id: 'd5', name: '凉拌鸡丝荞麦面', calories: 420, tags: ['清爽', '夏季首选'], ingredients: ['鸡胸肉', '黄瓜丝', '荞麦面', '蒜醋汁'], steps: ['鸡胸煮熟撕丝', '面条煮熟过凉水', '拌入蔬菜和料汁'] },
    { id: 'd6', name: '菌菇芙蓉蛋汤', calories: 280, tags: ['快手', '晚餐'], ingredients: ['香菇/海鲜菇', '鸡蛋 2个', '胡萝卜丝'], steps: ['菌菇炒香加水', '水开淋入蛋液', '加盐和胡椒粉调味'] },
    { id: 'd7', name: '轻食温沙拉', calories: 350, tags: ['维生素', '轻断食'], ingredients: ['羽衣甘蓝/生菜', '南瓜块', '煮鸡蛋', '油醋汁'], steps: ['南瓜烤熟', '蔬菜洗净', '混合所有食材淋汁'] },
  ]
};

const WEEK_DAYS = ['周一', '周二', '周三', '周四', '周五', '周六', '周日'];

// --- 辅助函数 ---
const shuffleArray = (array) => {
  const newArray = [...array];
  for (let i = newArray.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
  }
  return newArray;
};

const generateWeeklyPlan = () => {
  const plan = {};
  const shuffledBreakfast = shuffleArray([...RECIPE_DATABASE.breakfast]);
  const shuffledLunch = shuffleArray([...RECIPE_DATABASE.lunch]);
  const shuffledDinner = shuffleArray([...RECIPE_DATABASE.dinner]);

  WEEK_DAYS.forEach((day, index) => {
    plan[day] = {
      breakfast: shuffledBreakfast[index % shuffledBreakfast.length],
      lunch: shuffledLunch[index % shuffledLunch.length],
      dinner: shuffledDinner[index % shuffledDinner.length],
    };
  });
  return plan;
};

// --- 子组件: 标签胶囊 ---
const Tag = ({ text, type = 'default' }) => {
  const colors = {
    default: 'bg-gray-100 text-gray-600',
    highlight: 'bg-orange-100 text-orange-600',
    green: 'bg-green-100 text-green-600',
  };
  return (
    <span className={`text-xs px-2 py-1 rounded-full ${colors[type] || colors.default}`}>
      {text}
    </span>
  );
};

// --- 子组件: 详情弹窗 ---
const RecipeModal = ({ recipe, onClose }) => {
  if (!recipe) return null;

  return (
    <div className="fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4 animate-in fade-in duration-200">
      <div className="bg-white rounded-2xl w-full max-w-md max-h-[90vh] overflow-y-auto shadow-2xl flex flex-col">
        <div className="relative h-48 bg-orange-50 flex items-center justify-center rounded-t-2xl">
           <ChefHat size={64} className="text-orange-300" />
           <button 
            onClick={onClose}
            className="absolute top-4 right-4 p-2 bg-white/80 rounded-full hover:bg-white transition-colors"
           >
             <X size={20} className="text-gray-600" />
           </button>
        </div>
        
        <div className="p-6 flex-1">
          <div className="flex justify-between items-start mb-2">
            <h2 className="text-2xl font-bold text-gray-800">{recipe.name}</h2>
            <div className="flex items-center text-orange-500 font-semibold">
              <Flame size={16} className="mr-1" />
              {recipe.calories} kcal
            </div>
          </div>
          
          <div className="flex gap-2 mb-6 flex-wrap">
            {recipe.tags.map(tag => <Tag key={tag} text={tag} type="green" />)}
          </div>

          <div className="mb-6">
            <h3 className="text-lg font-semibold text-gray-700 mb-3 flex items-center">
              <ShoppingBag size={18} className="mr-2" /> 食材准备
            </h3>
            <ul className="space-y-2">
              {recipe.ingredients.map((item, idx) => (
                <li key={idx} className="flex items-center text-gray-600 text-sm">
                  <div className="w-1.5 h-1.5 rounded-full bg-orange-400 mr-2"></div>
                  {item}
                </li>
              ))}
            </ul>
          </div>

          <div>
            <h3 className="text-lg font-semibold text-gray-700 mb-3 flex items-center">
              <Clock size={18} className="mr-2" /> 制作步骤
            </h3>
            <div className="space-y-4">
              {recipe.steps.map((step, idx) => (
                <div key={idx} className="flex gap-3">
                  <div className="flex-shrink-0 w-6 h-6 rounded-full bg-orange-100 text-orange-600 flex items-center justify-center text-xs font-bold mt-0.5">
                    {idx + 1}
                  </div>
                  <p className="text-gray-600 text-sm leading-relaxed">{step}</p>
                </div>
              ))}
            </div>
          </div>
        </div>

        <div className="p-4 border-t border-gray-100">
          <button 
            onClick={onClose}
            className="w-full py-3 bg-orange-500 text-white rounded-xl font-medium hover:bg-orange-600 transition-colors"
          >
            我学会了
          </button>
        </div>
      </div>
    </div>
  );
};

// --- 主应用组件 ---
export default function WeeklyMealPlanner() {
  const [activeTab, setActiveTab] = useState('daily'); // daily, weekly, list, tips
  const [currentDayIndex, setCurrentDayIndex] = useState(0);
  const [weeklyPlan, setWeeklyPlan] = useState({});
  const [selectedRecipe, setSelectedRecipe] = useState(null);
  const [generatedList, setGeneratedList] = useState([]);

  // 初始化或重新生成计划
  useEffect(() => {
    const plan = generateWeeklyPlan();
    setWeeklyPlan(plan);
    generateShoppingList(plan);
  }, []);

  const regeneratePlan = () => {
    const newPlan = generateWeeklyPlan();
    setWeeklyPlan(newPlan);
    generateShoppingList(newPlan);
    // 简单的加载动画反馈
    const btn = document.getElementById('refresh-btn');
    if(btn) btn.classList.add('animate-spin');
    setTimeout(() => {
      if(btn) btn.classList.remove('animate-spin');
    }, 500);
  };

  const generateShoppingList = (plan) => {
    const list = [];
    Object.values(plan).forEach(day => {
      ['breakfast', 'lunch', 'dinner'].forEach(mealType => {
        day[mealType].ingredients.forEach(ing => {
          // 简单的去重逻辑，实际应用可能需要更复杂的解析
          if (!list.includes(ing)) {
            list.push(ing);
          }
        });
      });
    });
    setGeneratedList(list);
  };

  const currentDayName = WEEK_DAYS[currentDayIndex];
  const currentDayPlan = weeklyPlan[currentDayName];

  return (
    <div className="min-h-screen bg-gray-50 font-sans text-gray-800 pb-20 md:pb-0 md:pl-20">
      
      {/* 顶部导航 (Mobile) */}
      <header className="sticky top-0 z-30 bg-white/80 backdrop-blur-md border-b border-gray-100 px-4 py-4 flex justify-between items-center">
        <div>
          <h1 className="text-xl font-extrabold text-orange-600 flex items-center gap-2">
            <Utensils className="fill-orange-600 text-white" />
            好胃口
          </h1>
          <p className="text-xs text-gray-400">一周健康食谱计划</p>
        </div>
        <button 
          id="refresh-btn"
          onClick={regeneratePlan}
          className="p-2 bg-orange-50 text-orange-500 rounded-full hover:bg-orange-100 transition-colors"
          title="重新生成本周计划"
        >
          <RefreshCw size={20} />
        </button>
      </header>

      {/* 详情弹窗 */}
      <RecipeModal recipe={selectedRecipe} onClose={() => setSelectedRecipe(null)} />

      {/* 主要内容区域 */}
      <main className="max-w-3xl mx-auto p-4">
        
        {/* === TAB: 每日视图 === */}
        {activeTab === 'daily' && currentDayPlan && (
          <div className="space-y-6 animate-in slide-in-from-bottom-4 duration-300">
            {/* 日期选择器 */}
            <div className="flex justify-between items-center bg-white p-2 rounded-xl shadow-sm overflow-x-auto no-scrollbar">
              {WEEK_DAYS.map((day, idx) => (
                <button
                  key={day}
                  onClick={() => setCurrentDayIndex(idx)}
                  className={`flex-shrink-0 w-10 h-10 rounded-lg flex items-center justify-center text-sm font-medium transition-all ${
                    idx === currentDayIndex 
                      ? 'bg-orange-500 text-white shadow-md scale-110' 
                      : 'text-gray-400 hover:bg-gray-100'
                  }`}
                >
                  {day}
                </button>
              ))}
            </div>

            {/* 三餐卡片 */}
            <div className="space-y-4">
              {[
                { type: 'breakfast', title: '早餐', icon: <Clock size={18} />, color: 'text-yellow-600', bg: 'bg-yellow-50' },
                { type: 'lunch', title: '午餐', icon: <ChefHat size={18} />, color: 'text-orange-600', bg: 'bg-orange-50' },
                { type: 'dinner', title: '晚餐', icon: <Salad size={18} />, color: 'text-green-600', bg: 'bg-green-50' },
              ].map((meal) => {
                const recipe = currentDayPlan[meal.type];
                return (
                  <div 
                    key={meal.type}
                    onClick={() => setSelectedRecipe(recipe)}
                    className="group bg-white rounded-2xl p-5 shadow-sm border border-gray-100 hover:shadow-md transition-all cursor-pointer active:scale-[0.98]"
                  >
                    <div className="flex justify-between items-start mb-3">
                      <span className={`px-3 py-1 rounded-full text-xs font-bold flex items-center gap-1 ${meal.bg} ${meal.color}`}>
                        {meal.icon} {meal.title}
                      </span>
                      <ChevronRight size={18} className="text-gray-300 group-hover:text-orange-400 group-hover:translate-x-1 transition-all" />
                    </div>
                    
                    <h3 className="text-lg font-bold text-gray-800 mb-2">{recipe.name}</h3>
                    
                    <div className="flex items-center gap-3 text-sm text-gray-500 mb-3">
                      <span className="flex items-center gap-1">
                        <Flame size={14} /> {recipe.calories} kcal
                      </span>
                      <span className="w-1 h-1 rounded-full bg-gray-300"></span>
                      <span>{recipe.tags[0]}</span>
                    </div>

                    <div className="text-xs text-gray-400 line-clamp-1">
                      {recipe.ingredients.join(' · ')}
                    </div>
                  </div>
                );
              })}
            </div>

            {/* 营养小贴士 */}
            <div className="bg-blue-50 rounded-xl p-4 flex items-start gap-3">
              <Info className="text-blue-500 shrink-0 mt-0.5" size={20} />
              <div>
                <h4 className="font-bold text-blue-700 text-sm mb-1">今日营养建议</h4>
                <p className="text-blue-600/80 text-xs leading-relaxed">
                  记得多喝水！每餐之间补充水分有助于代谢。如果觉得胃口不好，可以尝试在饭前吃一点酸味水果（如橙子、山楂）开胃。
                </p>
              </div>
            </div>
          </div>
        )}

        {/* === TAB: 购物清单 === */}
        {activeTab === 'list' && (
          <div className="bg-white rounded-2xl shadow-sm p-6 min-h-[60vh] animate-in slide-in-from-right-4 duration-300">
            <h2 className="text-2xl font-bold mb-2 flex items-center gap-2">
              <ShoppingBag className="text-orange-500" /> 
              本周采购清单
            </h2>
            <p className="text-gray-400 text-sm mb-6">基于生成的周计划自动汇总</p>
            
            <div className="space-y-3">
              {generatedList.map((item, idx) => (
                <label key={idx} className="flex items-center p-3 rounded-lg hover:bg-gray-50 border border-transparent hover:border-gray-100 transition-colors cursor-pointer group">
                  <div className="relative flex items-center">
                    <input type="checkbox" className="peer w-5 h-5 rounded border-gray-300 text-orange-500 focus:ring-orange-500" />
                    <div className="absolute inset-0 hidden peer-checked:flex items-center justify-center pointer-events-none">
                      <CheckCircle2 size={20} className="text-orange-500 bg-white rounded-full" />
                    </div>
                  </div>
                  <span className="ml-3 text-gray-600 group-hover:text-gray-900 peer-checked:text-gray-400 peer-checked:line-through transition-colors">
                    {item}
                  </span>
                </label>
              ))}
            </div>
          </div>
        )}

        {/* === TAB: 健康与胃口改善 === */}
        {activeTab === 'tips' && (
          <div className="space-y-4 animate-in fade-in zoom-in-95 duration-300">
            <div className="bg-gradient-to-br from-orange-400 to-orange-600 rounded-2xl p-6 text-white shadow-lg">
              <h2 className="text-2xl font-bold mb-2">如何改善胃口？</h2>
              <p className="opacity-90">好的饮食习惯是健康的基础。</p>
            </div>

            <div className="grid gap-4">
              {[
                { title: '规律进食', content: '每天固定时间吃饭，让肠胃形成记忆，到点自然产生饥饿感。', icon: <Clock /> },
                { title: '色彩搭配', content: '五颜六色的食物（红番茄、绿蔬菜、黄鸡蛋）能从视觉上刺激食欲。', icon: <Heart /> },
                { title: '少食多餐', content: '如果一顿吃不下太多，可以分为4-5顿小餐，减轻肠胃负担。', icon: <Utensils /> },
                { title: '适度运动', content: '饭前一小时进行轻度运动（如散步），能有效促进新陈代谢和饥饿感。', icon: <Flame /> },
              ].map((tip, idx) => (
                <div key={idx} className="bg-white p-5 rounded-xl shadow-sm border border-gray-100">
                  <div className="w-10 h-10 bg-orange-100 rounded-full flex items-center justify-center text-orange-500 mb-3">
                    {tip.icon}
                  </div>
                  <h3 className="font-bold text-gray-800 mb-1">{tip.title}</h3>
                  <p className="text-sm text-gray-500">{tip.content}</p>
                </div>
              ))}
            </div>
          </div>
        )}

      </main>

      {/* 底部导航栏 (Mobile & Desktop Sidebar) */}
      <nav className="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200 px-6 py-3 md:top-0 md:bottom-auto md:w-20 md:h-screen md:flex-col md:border-t-0 md:border-r md:py-8 md:px-0 z-40">
        <div className="flex justify-between items-center md:flex-col md:gap-8 md:h-full">
          <div className="hidden md:block text-orange-600 mb-6">
            <ChefHat size={32} />
          </div>

          <div className="flex justify-between w-full md:flex-col md:gap-8">
            <button 
              onClick={() => setActiveTab('daily')}
              className={`flex flex-col items-center gap-1 transition-colors ${activeTab === 'daily' ? 'text-orange-500' : 'text-gray-400 hover:text-gray-600'}`}
            >
              <Calendar size={24} />
              <span className="text-[10px]">今日</span>
            </button>
            
            <button 
              onClick={() => setActiveTab('list')}
              className={`flex flex-col items-center gap-1 transition-colors ${activeTab === 'list' ? 'text-orange-500' : 'text-gray-400 hover:text-gray-600'}`}
            >
              <ShoppingBag size={24} />
              <span className="text-[10px]">采购</span>
            </button>

            <button 
              onClick={() => setActiveTab('tips')}
              className={`flex flex-col items-center gap-1 transition-colors ${activeTab === 'tips' ? 'text-orange-500' : 'text-gray-400 hover:text-gray-600'}`}
            >
              <Heart size={24} />
              <span className="text-[10px]">健康</span>
            </button>
          </div>
          
          <div className="hidden md:block mt-auto text-xs text-center text-gray-300">
            V1.0
          </div>
        </div>
      </nav>

    </div>
  );
}
