import React, { useState, useEffect } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { motion } from "framer-motion";

const questionsData = [
  {
    question: "What is the correct form of the verb: She ____ to campus every day.",
    options: ["go", "goes", "gone", "going"],
    answer: "goes",
    explanation:
      "Dalam Simple Present Tense, jika subjeknya 'She/He/It', maka kata kerja ditambah -s atau -es. Jadi jawabannya adalah 'goes'.",
  },
  {
    question: "Choose the correct sentence:",
    options: [
      "She don't like coffee.",
      "She doesn't likes coffee.",
      "She doesn't like coffee.",
      "She not like coffee.",
    ],
    answer: "She doesn't like coffee.",
    explanation:
      "Dalam kalimat negatif Simple Present untuk subjek She/He/It menggunakan 'does not (doesn't)' + verb 1 tanpa tambahan s.",
  },
  {
    question: "What is the synonym of 'Happy'?",
    options: ["Sad", "Angry", "Joyful", "Tired"],
    answer: "Joyful",
    explanation:
      "'Joyful' memiliki arti yang sama dengan 'Happy', yaitu merasa senang atau bahagia.",
  },
  {
    question: "Complete the sentence: They have lived here ____ 2020.",
    options: ["for", "since", "from", "at"],
    answer: "since",
    explanation:
      "'Since' digunakan untuk menunjukkan titik waktu tertentu (2020). Sedangkan 'for' digunakan untuk durasi waktu.",
  },
];

export default function QuizBahasaInggris() {
  const [name, setName] = useState("");
  const [started, setStarted] = useState(false);
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [score, setScore] = useState(0);
  const [selected, setSelected] = useState("");
  const [showExplanation, setShowExplanation] = useState(false);
  const [finished, setFinished] = useState(false);

  useEffect(() => {
    const savedScore = localStorage.getItem("quizScore");
    if (savedScore) {
      setScore(parseInt(savedScore));
    }
  }, []);

  const handleAnswer = (option) => {
    setSelected(option);
    setShowExplanation(true);
    if (option === questionsData[currentQuestion].answer) {
      const newScore = score + 25;
      setScore(newScore);
      localStorage.setItem("quizScore", newScore);
    }
  };

  const nextQuestion = () => {
    setSelected("");
    setShowExplanation(false);
    if (currentQuestion + 1 < questionsData.length) {
      setCurrentQuestion(currentQuestion + 1);
    } else {
      setFinished(true);
    }
  };

  const resetQuiz = () => {
    setScore(0);
    localStorage.removeItem("quizScore");
    setCurrentQuestion(0);
    setFinished(false);
    setStarted(false);
  };
