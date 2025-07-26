# Code-X
// Code X Web App - MVP v2 with Rewards and Login Placeholder import React, { useState } from 'react'; import { Card, CardContent } from '@/components/ui/card'; import { Button } from '@/components/ui/button'; import { Switch } from '@/components/ui/switch'; import { Input } from '@/components/ui/input'; import { motion } from 'framer-motion';

export default function CodeXApp() { const [darkMode, setDarkMode] = useState(true); const [hearts, setHearts] = useState(6); const [coins, setCoins] = useState(50); const [lesson, setLesson] = useState(1); const [streak, setStreak] = useState(3); const [rewardClaimed, setRewardClaimed] = useState(false);

const skipLesson = () => { if (hearts > 0) { setHearts(hearts - 1); setLesson(lesson + 1); } else { alert("You're out of hearts! Buy more or wait for refill."); } };

const completeLesson = () => { setLesson(lesson + 1); setStreak(streak + 1); };

const purchaseHeart = () => { if (coins >= 5) { setCoins(coins - 5); setHearts(hearts + 1); } else { alert("Not enough coins!"); } };

const claimDailyReward = () => { if (!rewardClaimed) { setCoins(coins + 10); setRewardClaimed(true); } else { alert("Reward already claimed today!"); } };

return ( <div className={darkMode ? 'bg-black text-gold min-h-screen p-4' : 'bg-white text-black min-h-screen p-4'}> <div className="flex justify-between items-center mb-4"> <h1 className="text-3xl font-bold">Code X</h1> <div className="flex items-center space-x-2"> <span>Dark Mode</span> <Switch checked={darkMode} onCheckedChange={setDarkMode} /> </div> </div>

{/* Placeholder for future login form */}
  {/* <Input placeholder="Email" /><Input placeholder="Password" type="password" /><Button>Login</Button> */}

  <Card className="mb-4">
    <CardContent>
      <h2 className="text-xl font-semibold">Lesson {lesson}</h2>
      <p>Complete your Python lesson for today.</p>
      <div className="mt-2 space-x-2">
        <Button onClick={completeLesson}>Complete</Button>
        <Button variant="destructive" onClick={skipLesson}>Skip (-1 ❤️)</Button>
      </div>
    </CardContent>
  </Card>

  <Card className="mb-4">
    <CardContent className="flex justify-between flex-col gap-2">
      <div>❤️ Hearts: {hearts}</div>
      <div>🪙 Coins: {coins}</div>
      <Button onClick={purchaseHeart}>Buy 1 ❤️ (5 coins)</Button>
    </CardContent>
  </Card>

  <Card className="mb-4">
    <CardContent>
      <h3 className="text-lg font-semibold">🔥 Streak: {streak} days</h3>
      <p>Keep your streak alive for bonus rewards!</p>
      <Button onClick={claimDailyReward}>Claim Daily Reward (+10 coins)</Button>
    </CardContent>
  </Card>

  <Card>
    <CardContent>
      <h3 className="text-lg font-semibold">🚀 Premium Lessons</h3>
      <p>These lessons require 20 coins to unlock.</p>
      <Button disabled={coins < 20}>Unlock Premium (20 coins)</Button>
    </CardContent>
  </Card>
</div>

); }

