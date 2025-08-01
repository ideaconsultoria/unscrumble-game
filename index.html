import React, { useState, useEffect } from 'react';
import { initializeApp } from 'firebase/app';
import { getAuth, signInWithCustomToken, onAuthStateChanged, signInAnonymously } from 'firebase/auth';
import { getFirestore, collection, onSnapshot, addDoc, doc, updateDoc, deleteDoc, query, where, getDocs } from 'firebase/firestore';

// Carrega as configurações do Firebase e o token de autenticação
const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';

// Cores para os blocos das palavras
const blockColors = [
  'bg-indigo-500', 'bg-blue-500', 'bg-green-500', 'bg-yellow-500', 'bg-red-500',
  'bg-purple-500', 'bg-pink-500', 'bg-teal-500', 'bg-orange-500', 'bg-cyan-500',
];

// Conjunto inicial de 40 frases (afirmativa, negativa, interrogativa)
const initialSentences = [
  // Likes and Dislikes (Presente Simples)
  { id: '1', text: 'I like to play video games on weekends' },
  { id: '2', text: 'She does not like to cook pasta at all' },
  { id: '3', text: 'Do you like to travel with your family?' },
  { id: '4', text: 'He really enjoys listening to rock music' },
  { id: '5', text: 'They do not enjoy eating spicy food' },
  { id: '6', text: 'Does your sister like to read fiction books?' },
  { id: '7', text: 'We love going to the beach on holidays' },
  { id: '8', text: 'He does not hate doing his homework' },
  // Routine (Presente Simples)
  { id: '9', text: 'We usually wake up at six in the morning' },
  { id: '10', text: 'I do not work on weekends' },
  { id: '11', text: 'Does she have lunch at twelve every day?' },
  { id: '12', text: 'They always brush their teeth before bed' },
  { id: '13', text: 'He does not take the bus to work' },
  { id: '14', text: 'Do we go to the gym on Fridays after work?' },
  { id: '15', text: 'My mom drives me to school every day' },
  { id: '16', text: 'I do not eat breakfast in the morning' },
  // Hobbies (Presente Contínuo)
  { id: '17', text: 'They are painting a beautiful picture right now' },
  { id: '18', text: 'I am not watching TV at the moment' },
  { id: '19', text: 'Are you listening to music on your headphones?' },
  { id: '20', text: 'He is playing guitar in his room' },
  { id: '21', text: 'We are not going to the movies tonight' },
  { id: '22', text: 'Is she knitting a scarf for winter?' },
  // Work Routine and Company (Presente Simples e Contínuo)
  { id: '23', text: 'The team is collaborating on the new project' },
  { id: '24', text: 'My colleague is not working from home today' },
  { id: '25', text: 'Is your boss giving you feedback right now?' },
  { id: '26', text: 'He works as an engineer for a big company' },
  { id: '27', text: 'They do not attend the weekly company meetings' },
  { id: '28', text: 'Does your company offer remote work?' },
  { id: '29', text: 'Our company is growing very fast this year' },
  { id: '30', text: 'The office is not open on national holidays' },
  // Talking about cities and style of living (Presente Simples)
  { id: '31', text: 'People in Brasília drive to every single place' },
  { id: '32', text: 'The traffic in Petrópolis is not very heavy' },
  { id: '33', text: 'Is the weather in Rio de Janeiro hot today?' },
  { id: '34', text: 'São Paulo has many beautiful green parks' },
  { id: '35', text: 'They are not living in the city center at all' },
  // Brasília (Presente Simples e Contínuo)
  { id: '36', text: 'Brasília has a very unique architectural style' },
  { id: '37', text: 'My family is not visiting Brasília this month' },
  { id: '38', text: 'Is the architecture in Brasília very modern?' },
  { id: '39', text: 'We are sightseeing around the city now' },
  // Petrópolis (Presente Simples e Contínuo)
  { id: '40', text: 'Petrópolis is also known as the Imperial City' },
  { id: '41', text: 'We are not hiking in Petrópolis this weekend' },
  { id: '42', text: 'Are you going to the Crystal Palace in Petrópolis?' },
];

// Componente principal do aplicativo
export default function App() {
  const [db, setDb] = useState(null);
  const [auth, setAuth] = useState(null);
  const [userId, setUserId] = useState(null);
  const [role, setRole] = useState('student');
  const [loading, setLoading] = useState(true);
  const [sentences, setSentences] = useState([]);
  const [submissions, setSubmissions] = useState([]);
  const [isModalOpen, setIsModalOpen] = useState(false);
  const [modalMessage, setModalMessage] = useState('');
  const [professorId, setProfessorId] = useState(null);

  // 1. Inicializa o Firebase e autentica o usuário
  useEffect(() => {
    const initFirebase = async () => {
      try {
        const app = initializeApp(firebaseConfig);
        const firestore = getFirestore(app);
        const authService = getAuth(app);

        // Define o papel e o ID do professor com base na URL
        const urlParams = new URLSearchParams(window.location.search);
        const roleFromUrl = urlParams.get('role');
        const professorIdFromUrl = urlParams.get('professorId');

        if (roleFromUrl === 'professor') {
          setRole('professor');
        } else if (professorIdFromUrl) {
          setProfessorId(professorIdFromUrl);
        }

        if (initialAuthToken) {
          await signInWithCustomToken(authService, initialAuthToken);
        } else {
          await signInAnonymously(authService);
        }

        onAuthStateChanged(authService, (user) => {
          if (user) {
            setUserId(user.uid);
          }
          setDb(firestore);
          setAuth(authService);
          setLoading(false);
        });
      } catch (error) {
        console.error("Erro ao inicializar o Firebase:", error);
        setLoading(false);
      }
    };

    initFirebase();
  }, []);

  // 2. Escuta as frases do professor em tempo real e combina com as frases iniciais
  useEffect(() => {
    if (db && userId) {
      if (role === 'professor') {
        const q = query(collection(db, `/artifacts/${appId}/users/${userId}/sentences`));
        const unsubscribe = onSnapshot(q, (snapshot) => {
          const sentencesData = snapshot.docs.map(doc => ({
            id: doc.id,
            ...doc.data(),
          }));
          setSentences([...initialSentences, ...sentencesData]);
        }, (error) => {
          console.error("Erro ao carregar frases do professor:", error);
        });
        return () => unsubscribe();
      } else {
        // Aluno recebe as frases iniciais e as frases do professor
        if (professorId) {
            const q = query(collection(db, `/artifacts/${appId}/users/${professorId}/sentences`));
            const unsubscribe = onSnapshot(q, (snapshot) => {
              const sentencesData = snapshot.docs.map(doc => ({
                id: doc.id,
                ...doc.data(),
              }));
              setSentences([...initialSentences, ...sentencesData]);
            }, (error) => {
              console.error("Erro ao carregar frases do professor para o aluno:", error);
            });
            return () => unsubscribe();
        } else {
            // Se não houver professorId, o aluno joga apenas com as frases iniciais
            setSentences(initialSentences);
        }
      }
    }
  }, [db, role, userId, appId, professorId]);

  // 3. Escuta as submissões dos alunos em tempo real (para o professor)
  useEffect(() => {
    if (db && role === 'professor' && userId) {
      const q = query(collection(db, `/artifacts/${appId}/users/${userId}/submissions`));
      const unsubscribe = onSnapshot(q, (snapshot) => {
        const submissionsData = snapshot.docs.map(doc => ({
          id: doc.id,
          ...doc.data(),
        }));
        setSubmissions(submissionsData);
      }, (error) => {
        console.error("Erro ao carregar submissões:", error);
      });
      return () => unsubscribe();
    }
  }, [db, role, userId, appId]);

  // Exibe tela de carregamento
  if (loading) {
    return <div className="flex items-center justify-center min-h-screen bg-gray-100">Carregando...</div>;
  }

  return (
    <div className="bg-gray-100 min-h-screen flex flex-col items-center justify-center p-4">
      <div className="max-w-4xl w-full bg-white rounded-xl shadow-2xl p-8 space-y-8">
        <header className="text-center">
          <h1 className="text-4xl md:text-5xl font-extrabold text-gray-800">
            Uscrumble
          </h1>
          <p className="text-lg text-gray-600 mt-2">
            Acesse o jogo com o seu link de professor ou aluno.
          </p>
        </header>

        {role === 'professor' ? (
          <ProfessorView db={db} userId={userId} sentences={sentences} submissions={submissions} appId={appId} blockColors={blockColors} setModalMessage={setModalMessage} setIsModalOpen={setIsModalOpen} />
        ) : (
          <StudentView db={db} userId={userId} sentences={sentences} appId={appId} blockColors={blockColors} setModalMessage={setModalMessage} setIsModalOpen={setIsModalOpen} professorId={professorId} />
        )}
      </div>
      {/* Modal para mensagens de sucesso/erro */}
      {isModalOpen && (
        <div className="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center p-4">
          <div className="bg-white rounded-xl shadow-2xl p-6 max-w-sm w-full text-center">
            <p className="text-lg font-semibold text-gray-800">{modalMessage}</p>
            <button
              onClick={() => setIsModalOpen(false)}
              className="mt-4 px-6 py-2 bg-indigo-600 text-white font-bold rounded-full hover:bg-indigo-700 transition-colors"
            >
              Fechar
            </button>
          </div>
        </div>
      )}
    </div>
  );
}

// Componente de arrastar e soltar
const DragAndDropGame = ({ sentence, onComplete, blockColors, savedProgress }) => {
  const [scrambledWords, setScrambledWords] = useState([]);
  const [targetWords, setTargetWords] = useState([]);
  const [isCorrect, setIsCorrect] = useState(false);

  useEffect(() => {
    if (sentence) {
      if (savedProgress) {
        setScrambledWords(savedProgress.scrambled);
        setTargetWords(savedProgress.target);
        // Atualiza o estado de correção se a frase estiver completa
        const studentAnswer = savedProgress.target.map(w => w.text).join(' ');
        setIsCorrect(studentAnswer === sentence.text);
      } else {
        const words = sentence.text.split(' ').map((word, index) => ({
          text: word,
          id: `${word}-${index}`,
          color: blockColors[index % blockColors.length]
        }));
        const shuffledWords = [...words].sort(() => Math.random() - 0.5);
        setScrambledWords(shuffledWords);
        setTargetWords(Array(words.length).fill(null));
        setIsCorrect(false);
      }
    }
  }, [sentence, savedProgress, blockColors]);

  const handleDragStart = (e, word) => {
    e.dataTransfer.setData('wordId', word.id);
  };

  const handleDragOver = (e) => {
    e.preventDefault();
  };

  const handleDrop = (e, targetIndex) => {
    e.preventDefault();
    const wordId = e.dataTransfer.getData('wordId');
    const word = scrambledWords.find(w => w.id === wordId);

    if (word) {
      const newTargetWords = [...targetWords];
      const newScrambledWords = scrambledWords.filter(w => w.id !== wordId);

      if (newTargetWords[targetIndex] === null) {
        newTargetWords[targetIndex] = word;
      } else {
        const oldWord = newTargetWords[targetIndex];
        newScrambledWords.push(oldWord);
        newTargetWords[targetIndex] = word;
      }

      setScrambledWords(newScrambledWords);
      setTargetWords(newTargetWords);

      if (newTargetWords.every(w => w !== null) && onComplete) {
        const currentSentence = newTargetWords.map(w => w.text).join(' ');
        const isGameCorrect = currentSentence === sentence.text;
        setIsCorrect(isGameCorrect);
        onComplete(isGameCorrect, currentSentence, { scrambled: newScrambledWords, target: newTargetWords });
      }
    }
  };

  return (
    <div className="flex flex-col space-y-6">
      {sentence && (
        <>
          <div className="p-4 bg-gray-200 rounded-xl shadow-inner">
            <h3 className="text-xl font-semibold text-gray-700 mb-2">Arraste as palavras para a ordem correta:</h3>
            <div className="flex flex-wrap gap-2">
              {scrambledWords.map((word) => (
                <div
                  key={word.id}
                  draggable
                  onDragStart={(e) => handleDragStart(e, word)}
                  className={`px-4 py-2 rounded-lg text-white font-bold cursor-grab active:cursor-grabbing transform hover:scale-105 transition-transform shadow-md ${word.color}`}
                >
                  {word.text}
                </div>
              ))}
            </div>
          </div>
          <div className="p-4 bg-gray-200 rounded-xl shadow-inner">
            <h3 className="text-xl font-semibold text-gray-700 mb-2">Construa a frase aqui:</h3>
            <div className="flex flex-wrap gap-2 min-h-[50px]">
              {targetWords.map((word, index) => (
                <div
                  key={index}
                  onDragOver={handleDragOver}
                  onDrop={(e) => handleDrop(e, index)}
                  className={`flex items-center justify-center border-2 border-dashed rounded-lg p-2 transition-colors ${word ? word.color : 'border-gray-400 bg-gray-100 hover:bg-gray-200'}`}
                  style={{ minWidth: '100px', minHeight: '48px' }}
                >
                  {word && <span className="text-white font-bold">{word.text}</span>}
                </div>
              ))}
            </div>
          </div>
        </>
      )}
    </div>
  );
};

// Componente da interface do Professor
const ProfessorView = ({ db, userId, sentences, submissions, appId, setModalMessage, setIsModalOpen }) => {
  const [newSentenceText, setNewSentenceText] = useState('');
  const [editSentenceId, setEditSentenceId] = useState(null);
  const [editSentenceText, setEditSentenceText] = useState('');

  // Adiciona uma nova frase
  const handleAddSentence = async (e) => {
    e.preventDefault();
    if (newSentenceText.trim() === '') return;
    try {
      // Salva a nova frase na coleção do professor.
      const sentencesCollectionRef = collection(db, `/artifacts/${appId}/users/${userId}/sentences`);
      await addDoc(sentencesCollectionRef, { text: newSentenceText.trim(), createdAt: new Date() });
      setNewSentenceText('');
      setModalMessage("Frase adicionada com sucesso!");
      setIsModalOpen(true);
    } catch (error) {
      console.error("Erro ao adicionar frase:", error);
      setModalMessage("Erro ao adicionar frase. Tente novamente.");
      setIsModalOpen(true);
    }
  };

  // Prepara para editar uma frase
  const startEdit = (sentence) => {
    setEditSentenceId(sentence.id);
    setEditSentenceText(sentence.text);
  };

  // Salva a edição da frase
  const saveEdit = async (id) => {
    if (editSentenceText.trim() === '') return;
    try {
      const sentenceDocRef = doc(db, `/artifacts/${appId}/users/${userId}/sentences`, id);
      await updateDoc(sentenceDocRef, { text: editSentenceText.trim() });
      setEditSentenceId(null);
      setEditSentenceText('');
      setModalMessage("Frase atualizada com sucesso!");
      setIsModalOpen(true);
    } catch (error) {
      console.error("Erro ao atualizar frase:", error);
      setModalMessage("Erro ao atualizar frase. Tente novamente.");
      setIsModalOpen(true);
    }
  };

  // Cancela a edição
  const cancelEdit = () => {
    setEditSentenceId(null);
    setEditSentenceText('');
  };

  // Exclui uma frase
  const handleDeleteSentence = async (id) => {
    if (window.confirm("Tem certeza que deseja excluir esta frase?")) {
      try {
        const sentenceDocRef = doc(db, `/artifacts/${appId}/users/${userId}/sentences`, id);
        await deleteDoc(sentenceDocRef);
        setModalMessage("Frase excluída com sucesso!");
        setIsModalOpen(true);
      } catch (error) {
        console.error("Erro ao excluir frase:", error);
        setModalMessage("Erro ao excluir frase. Tente novamente.");
        setIsModalOpen(true);
      }
    }
  };

  return (
    <div className="space-y-8">
      <h2 className="text-3xl font-bold text-gray-800 text-center">Interface do Professor</h2>
      <div className="bg-gray-50 p-6 rounded-xl shadow-md">
        <h3 className="text-2xl font-semibold text-gray-700 mb-4">Gerenciar Frases</h3>
        <p className="text-sm text-gray-500 mb-4">Seu ID de Professor para compartilhar com alunos: <span className="font-mono bg-gray-200 rounded-md px-2 py-1">{userId}</span></p>
        <form onSubmit={handleAddSentence} className="flex flex-col md:flex-row gap-4">
          <input
            type="text"
            value={newSentenceText}
            onChange={(e) => setNewSentenceText(e.target.value)}
            placeholder="Digite uma nova frase aqui..."
            className="flex-1 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500"
          />
          <button
            type="submit"
            className="px-6 py-3 bg-indigo-600 text-white font-bold rounded-lg hover:bg-indigo-700 transition-colors"
          >
            Adicionar Frase
          </button>
        </form>

        <ul className="mt-6 space-y-4">
          {sentences.map((sentence) => (
            <li key={sentence.id} className="flex items-center justify-between p-4 bg-white rounded-lg shadow-sm">
              {editSentenceId === sentence.id ? (
                <>
                  <input
                    type="text"
                    value={editSentenceText}
                    onChange={(e) => setEditSentenceText(e.target.value)}
                    className="flex-1 p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500"
                  />
                  <div className="flex space-x-2 ml-4">
                    <button onClick={() => saveEdit(sentence.id)} className="px-4 py-2 bg-green-500 text-white rounded-lg hover:bg-green-600 transition-colors">
                      Salvar
                    </button>
                    <button onClick={cancelEdit} className="px-4 py-2 bg-gray-500 text-white rounded-lg hover:bg-gray-600 transition-colors">
                      Cancelar
                    </button>
                  </div>
                </>
              ) : (
                <>
                  <span className="text-lg text-gray-800">{sentence.text}</span>
                  <div className="flex space-x-2">
                    <button onClick={() => startEdit(sentence)} className="px-4 py-2 bg-yellow-500 text-white rounded-lg hover:bg-yellow-600 transition-colors">
                      Editar
                    </button>
                    <button onClick={() => handleDeleteSentence(sentence.id)} className="px-4 py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition-colors">
                      Excluir
                    </button>
                  </div>
                </>
              )}
            </li>
          ))}
        </ul>
      </div>

      <div className="bg-gray-50 p-6 rounded-xl shadow-md mt-8">
        <h3 className="text-2xl font-semibold text-gray-700 mb-4">Submissões dos Alunos</h3>
        <p className="text-sm text-gray-500 mb-4">ID do Professor: <span className="font-mono bg-gray-200 rounded-md px-2 py-1">{userId}</span></p>
        <ul className="space-y-4">
          {submissions.length > 0 ? (
            submissions.map((submission) => (
              <li key={submission.id} className="p-4 bg-white rounded-lg shadow-sm">
                <p className="font-bold text-lg text-gray-800">Aluno: {submission.studentId}</p>
                <p className="text-gray-600">Enviado em: {new Date(submission.submittedAt.toDate()).toLocaleString()}</p>
                <div className="mt-2 space-y-1">
                  {submission.results.map((result, index) => (
                    <div key={index} className="p-3 bg-gray-100 rounded-md">
                      <p className="font-semibold text-gray-700">Frase Original: <span className="font-normal">{result.originalSentence}</span></p>
                      <p className="font-semibold text-gray-700">Resposta do Aluno: <span className="font-normal">{result.studentAnswer}</span></p>
                      <p className="font-semibold text-gray-700">Status: <span className={`${result.isCorrect ? 'text-green-500' : 'text-red-500'} font-bold`}>{result.isCorrect ? 'Correto' : 'Incorreto'}</span></p>
                    </div>
                  ))}
                </div>
              </li>
            ))
          ) : (
            <p className="text-gray-500">Nenhuma submissão de aluno encontrada.</p>
          )}
        </ul>
      </div>
    </div>
  );
};

// Componente da interface do Aluno
const StudentView = ({ db, userId, sentences, appId, blockColors, setModalMessage, setIsModalOpen, professorId }) => {
  const [currentSentenceIndex, setCurrentSentenceIndex] = useState(0);
  const [progress, setProgress] = useState(Array(sentences.length).fill(null));
  const [stats, setStats] = useState({ correct: 0, incorrect: 0, total: 0 });

  useEffect(() => {
    if (sentences.length > 0) {
      setProgress(Array(sentences.length).fill(null));
      setStats({ correct: 0, incorrect: 0, total: 0 });
      setCurrentSentenceIndex(0);
    }
  }, [sentences]);

  const handleSentenceComplete = (isCorrect, studentAnswer, savedState) => {
    const newProgress = [...progress];
    newProgress[currentSentenceIndex] = {
      originalSentence: sentences[currentSentenceIndex].text,
      studentAnswer: studentAnswer,
      isCorrect,
      ...savedState,
    };
    setProgress(newProgress);

    setStats(prevStats => ({
      ...prevStats,
      total: newProgress.filter(p => p !== null).length,
      correct: newProgress.filter(p => p && p.isCorrect).length,
      incorrect: newProgress.filter(p => p && !p.isCorrect).length,
    }));
  };

  const saveProgress = async () => {
    try {
      const progressCollectionRef = collection(db, `/artifacts/${appId}/users/${userId}/progress`);
      const q = query(progressCollectionRef, where("studentId", "==", userId));
      const querySnapshot = await getDocs(q);

      const savedProgressData = progress.filter(p => p !== null);

      if (!querySnapshot.empty) {
        const docId = querySnapshot.docs[0].id;
        const docRef = doc(progressCollectionRef, docId);
        await updateDoc(docRef, {
          progress: savedProgressData,
          updatedAt: new Date(),
        });
      } else {
        await addDoc(progressCollectionRef, {
          studentId: userId,
          progress: savedProgressData,
          createdAt: new Date(),
        });
      }
      setModalMessage("Progresso salvo com sucesso!");
      setIsModalOpen(true);
    } catch (error) {
      console.error("Erro ao salvar progresso:", error);
      setModalMessage("Erro ao salvar progresso. Tente novamente.");
      setIsModalOpen(true);
    }
  };

  const handleSubmit = async () => {
    try {
      if (progress.length === 0) {
        setModalMessage("Nenhuma frase para enviar.");
        setIsModalOpen(true);
        return;
      }
      // O aluno envia as respostas para a coleção do professor
      const submissionsCollectionRef = collection(db, `/artifacts/${appId}/users/${professorId}/submissions`);
      await addDoc(submissionsCollectionRef, {
        studentId: userId,
        results: progress,
        submittedAt: new Date(),
      });
      setModalMessage("Respostas enviadas com sucesso! Seu professor poderá visualizá-las.");
      setIsModalOpen(true);
    } catch (error) {
      console.error("Erro ao enviar respostas:", error);
      setModalMessage("Erro ao enviar respostas. Tente novamente.");
      setIsModalOpen(true);
    }
  };

  const nextSentence = () => {
    if (currentSentenceIndex < sentences.length - 1) {
      setCurrentSentenceIndex(currentSentenceIndex + 1);
    }
  };

  const prevSentence = () => {
    if (currentSentenceIndex > 0) {
      setCurrentSentenceIndex(currentSentenceIndex - 1);
    }
  };

  const currentSentence = sentences[currentSentenceIndex];

  return (
    <div className="space-y-8">
      <h2 className="text-3xl font-bold text-gray-800 text-center">Interface do Aluno</h2>
      <p className="text-lg text-gray-600 text-center">ID do Aluno: <span className="font-mono bg-gray-200 rounded-md px-2 py-1">{userId}</span></p>

      {sentences.length > 0 ? (
        <>
          <div className="bg-gray-50 p-6 rounded-xl shadow-md">
            <h3 className="text-2xl font-semibold text-gray-700 mb-4">
              Frase {currentSentenceIndex + 1} de {sentences.length}
            </h3>
            <DragAndDropGame
              sentence={currentSentence}
              onComplete={handleSentenceComplete}
              blockColors={blockColors}
              savedProgress={progress[currentSentenceIndex]}
            />
          </div>

          <div className="flex flex-col md:flex-row justify-between items-center gap-4">
            <div className="flex gap-4">
              <button
                onClick={prevSentence}
                disabled={currentSentenceIndex === 0}
                className="px-6 py-3 bg-gray-200 text-gray-800 font-bold rounded-full disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
              >
                Anterior
              </button>
              <button
                onClick={nextSentence}
                disabled={currentSentenceIndex === sentences.length - 1}
                className="px-6 py-3 bg-gray-200 text-gray-800 font-bold rounded-full disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
              >
                Próxima
              </button>
            </div>
            <div className="flex flex-col sm:flex-row gap-4 w-full md:w-auto">
              <button
                onClick={saveProgress}
                className="w-full sm:w-auto px-6 py-3 bg-yellow-500 text-white font-bold rounded-full hover:bg-yellow-600 transition-colors"
              >
                Salvar Progresso
              </button>
              <button
                onClick={handleSubmit}
                className="w-full sm:w-auto px-6 py-3 bg-indigo-600 text-white font-bold rounded-full hover:bg-indigo-700 transition-colors"
              >
                Submeter Respostas Finais
              </button>
            </div>
          </div>
        </>
      ) : (
        <p className="text-center text-lg text-gray-600">Nenhuma frase disponível para jogar.</p>
      )}

      <div className="bg-gray-50 p-6 rounded-xl shadow-md mt-8">
        <h3 className="text-2xl font-semibold text-gray-700 mb-4">Estatísticas do Jogo</h3>
        <div className="flex flex-wrap justify-around text-center gap-4">
          <div className="p-4 bg-indigo-100 rounded-lg flex-1 min-w-[150px]">
            <p className="text-4xl font-bold text-indigo-600">{stats.total}</p>
            <p className="text-gray-600">Frases Concluídas</p>
          </div>
          <div className="p-4 bg-green-100 rounded-lg flex-1 min-w-[150px]">
            <p className="text-4xl font-bold text-green-600">{stats.correct}</p>
            <p className="text-gray-600">Respostas Corretas</p>
          </div>
          <div className="p-4 bg-red-100 rounded-lg flex-1 min-w-[150px]">
            <p className="text-4xl font-bold text-red-600">{stats.incorrect}</p>
            <p className="text-gray-600">Respostas Incorretas</p>
          </div>
        </div>
      </div>
    </div>
  );
};# unscrumble-game
