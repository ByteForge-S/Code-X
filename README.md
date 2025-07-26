# Code
import React, { useState, useEffect } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button"; import { Moon, Sun, Flame, Heart, Coins } from "lucide-react"; import { motion } from "framer-motion";

const lessons = [ "Introduction to Python", "Variables & Data Types", "Control Structures", "Functions", "Loops", "Projects" ];

export default function CodeXApp() { const [darkMode, setDarkMode] = useState(true); const [hearts, setHearts] = useState(6); const [coins, setCoins] = useState(50); const [completedLessons, setCompletedLessons] = useState([]); const [streak, setStreak] = useState(1);

useEffect(() => { document.body.className = darkMode ? "bg-black text-white" : "bg-white text-black"; }, [darkMode]);

const handleLessonAction = (lesson, action) => { if (action === "skip") { if (hearts > 0) setHearts(hearts - 1); } else if (action === "complete") { if (!completedLessons.includes(lesson)) { setCompletedLessons([...completedLessons, lesson]); setCoins(coins + 5); } } };

const buyHeart = () => { if (coins >= 10 && hearts < 6) { setCoins(coins - 10); setHearts(hearts + 1); } };

return ( <div className="min-h-screen p-4 space-y-4"> <div className="flex justify-between items-center"> <h1 className="text-2xl font-bold">Code X</h1> <Button variant="ghost" onClick={() => setDarkMode(!darkMode)}> {darkMode ? <Sun size={20} /> : <Moon size={20} />} </Button> </div>

<div className="flex gap-4 items-center">
    <div className="flex items-center gap-1">
      <Heart className="text-red-500" /> {hearts}
    </div>
    <div className="flex items-center gap-1">
      <Coins className="text-yellow-400" /> {coins}
    </div>
    <div className="flex items-center gap-1">
      <Flame className="text-orange-500" /> Streak: {streak}
    </div>
  </div>

  <div className="grid gap-4">
    {lessons.map((lesson) => (
      <Card key={lesson} className="shadow-xl">
        <CardContent className="flex justify-between items-center p-4">
          <div>{lesson}</div>
          <div className="flex gap-2">
            <Button onClick={() => handleLessonAction(lesson, "complete")}>
              Complete
            </Button>
            <Button variant="destructive" onClick={() => handleLessonAction(lesson, "skip")}>Skip</Button>
          </div>
        </CardContent>
      </Card>
    ))}
  </div>

  <div className="mt-4 text-center">
    <Button onClick={buyHeart}>Buy Heart (10 Coins)</Button>
  </div>
</div>

); }

