import React, { useState, useEffect } from 'react';
import { Card, CardHeader, CardContent, CardFooter } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Tabs, TabsList, TabsTrigger, TabsContent } from '@/components/ui/tabs';
import { MapPin, Heart, MessageCircle, Shield, Star, Bot, Send, User } from 'lucide-react';
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from '@/components/ui/select';

// Composant Assistant IA
const AIAssistant = ({ isOpen, onClose }) => {
  const [messages, setMessages] = useState([
    {
      type: 'ai',
      content: "Bonjour ! Je suis votre assistant personnel. Je peux vous aider à :\n- Trouver des profils compatibles\n- Améliorer votre profil\n- Donner des conseils de conversation\nQue puis-je faire pour vous ?"
    }
  ]);
  const [inputMessage, setInputMessage] = useState('');
  const [isTyping, setIsTyping] = useState(false);

  // Simuler les réponses de l'IA
  const aiResponses = {
    profile: [
      "Voici quelques conseils pour améliorer votre profil :",
      "- Ajoutez une photo récente et de qualité",
      "- Décrivez vos passions de manière authentique",
      "- Partagez vos centres d'intérêt",
      "Voulez-vous que je vous aide à rédiger une bio attractive ?"
    ],
    match: [
      "D'après vos centres d'intérêt, voici les profils qui pourraient vous correspondre :",
      "- Sarah aime aussi la lecture et la cuisine",
      "- Marc partage votre passion pour l'art",
      "Souhaitez-vous que j'analyse plus en détail ces compatibilités ?"
    ],
    conversation: [
      "Pour démarrer une conversation, je suggère :",
      "- Mentionnez un intérêt commun",
      "- Posez une question ouverte",
      "- Restez naturel et authentique",
      "Voulez-vous des exemples de messages d'ouverture ?"
    ]
  };

  const handleSendMessage = async () => {
    if (!inputMessage.trim()) return;

    // Ajouter le message de l'utilisateur
    const userMessage = { type: 'user', content: inputMessage };
    setMessages(prev => [...prev, userMessage]);
    setInputMessage('');
    setIsTyping(true);

    // Simuler le traitement de l'IA
    setTimeout(() => {
      let response = "Je ne suis pas sûr de comprendre. Pouvez-vous reformuler ?";
      
      // Analyse simple du message pour déterminer la réponse
      const lowercaseInput = inputMessage.toLowerCase();
      if (lowercaseInput.includes('profil')) {
        response = aiResponses.profile.join('\n');
      } else if (lowercaseInput.includes('match') || lowercaseInput.includes('compatib')) {
        response = aiResponses.match.join('\n');
      } else if (lowercaseInput.includes('message') || lowercaseInput.includes('conversation')) {
        response = aiResponses.conversation.join('\n');
      }

      setMessages(prev => [...prev, { type: 'ai', content: response }]);
      setIsTyping(false);
    }, 1000);
  };

  return (
    <Card className={`fixed bottom-4 right-4 w-96 h-[500px] shadow-xl ${isOpen ? 'flex' : 'hidden'} flex-col`}>
      <CardHeader className="bg-purple-600 text-white p-4 rounded-t-lg">
        <div className="flex items-center justify-between">
          <div className="flex items-center gap-2">
            <Bot size={24} />
            <h3 className="font-bold">Assistant IA</h3>
          </div>
          <Button variant="ghost" className="text-white hover:text-purple-200" onClick={onClose}>
            ✕
          </Button>
        </div>
      </CardHeader>
      
      <CardContent className="flex-1 overflow-y-auto p-4 space-y-4">
        {messages.map((message, index) => (
          <div
            key={index}
            className={`flex ${message.type === 'user' ? 'justify-end' : 'justify-start'}`}
          >
            <div
              className={`max-w-[80%] p-3 rounded-lg ${
                message.type === 'user'
                  ? 'bg-purple-600 text-white'
                  : 'bg-gray-100 text-gray-800'
              }`}
            >
              <div className="flex items-center gap-2 mb-1">
                {message.type === 'ai' ? <Bot size={16} /> : <User size={16} />}
                <span className="font-semibold">
                  {message.type === 'ai' ? 'Assistant' : 'Vous'}
                </span>
              </div>
              <p className="whitespace-pre-line">{message.content}</p>
            </div>
          </div>
        ))}
        {isTyping && (
          <div className="flex items-center gap-2 text-gray-500">
            <Bot size={16} />
            <span>L'assistant écrit...</span>
          </div>
        )}
      </CardContent>

      <CardFooter className="p-4 border-t">
        <div className="flex w-full gap-2">
          <Input
            value={inputMessage}
            onChange={(e) => setInputMessage(e.target.value)}
            placeholder="Posez votre question..."
            onKeyPress={(e) => e.key === 'Enter' && handleSendMessage()}
          />
          <Button onClick={handleSendMessage}>
            <Send size={16} />
          </Button>
        </div>
      </CardFooter>
    </Card>
  );
};

// Composant Principal
const App = () => {
  const [selectedCity, setSelectedCity] = useState('ouaga');
  const [searchQuery, setSearchQuery] = useState('');
  const [isAIOpen, setIsAIOpen] = useState(false);

  const cities = [
    { id: 'ouaga', name: 'Ouagadougou' },
    { id: 'bobo', name: 'Bobo-Dioulasso' },
    { id: 'koudougou', name: 'Koudougou' },
    { id: 'banfora', name: 'Banfora' }
  ];

  const profiles = [
    {
      id: 1,
      name: 'Sarah K.',
      age: 24,
      city: 'Ouagadougou',
      interests: ['Sport', 'Lecture', 'Cuisine'],
      verified: true,
      compatibilityScore: 85
    },
    {
      id: 2,
      name: 'Marc O.',
      age: 28,
      city: 'Bobo-Dioulasso',
      interests: ['Musique', 'Voyage', 'Art'],
      verified: true,
      compatibilityScore: 78
    }
  ];

  return (
    <div className="min-h-screen bg-gray-100 p-4">
      <div className="max-w-4xl mx-auto bg-white rounded-lg shadow-md p-4 mb-4">
        <div className="flex justify-between items-center mb-4">
          <h1 className="text-2xl font-bold text-purple-600">
            Rencontres Amicales Burkina
          </h1>
          <Button
            onClick={() => setIsAIOpen(true)}
            className="flex items-center gap-2 bg-purple-600 hover:bg-purple-700"
          >
            <Bot size={16} />
            Assistant IA
          </Button>
        </div>
        
        <div className="flex items-center gap-2 mb-4">
          <MapPin className="text-gray-500" />
          <Select value={selectedCity} onValueChange={setSelectedCity}>
            <SelectTrigger className="w-[200px]">
              <SelectValue placeholder="Sélectionnez une ville" />
            </SelectTrigger>
            <SelectContent>
              {cities.map(city => (
                <SelectItem key={city.id} value={city.id}>
                  {city.name}
                </SelectItem>
              ))}
            </SelectContent>
          </Select>
        </div>

        <div className="relative mb-4">
          <Input
            type="search"
            placeholder="Rechercher des profils..."
            value={searchQuery}
            onChange={(e) => setSearchQuery(e.target.value)}
            className="w-full"
          />
        </div>
      </div>

      <div className="max-w-4xl mx-auto">
        <Tabs defaultValue="explore" className="w-full">
          <TabsList className="grid w-full grid-cols-4 gap-4">
            <TabsTrigger value="explore">Explorer</TabsTrigger>
            <TabsTrigger value="messages">Messages</TabsTrigger>
            <TabsTrigger value="likes">J'aime</TabsTrigger>
            <TabsTrigger value="profile">Profil</TabsTrigger>
          </TabsList>

          <TabsContent value="explore">
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              {profiles.map(profile => (
                <Card key={profile.id}>
                  <CardHeader>
                    <div className="flex justify-between items-center">
                      <div>
                        <h3 className="font-bold">{profile.name}, {profile.age}</h3>
                        <p className="text-sm text-gray-500 flex items-center">
                          <MapPin className="mr-1" size={16} />
                          {profile.city}
                        </p>
                      </div>
                      <div className="flex items-center gap-2">
                        {profile.verified && (
                          <Shield className="text-blue-500" size={20} />
                        )}
                        <span className="text-sm font-medium text-green-600">
                          {profile.compatibilityScore}% compatible
                        </span>
                      </div>
                    </div>
                  </CardHeader>
                  <CardContent>
                    <div className="flex flex-wrap gap-2 mb-4">
                      {profile.interests.map(interest => (
                        <span key={interest} className="bg-purple-100 text-purple-600 px-2 py-1 rounded-full text-sm">
                          {interest}
                        </span>
                      ))}
                    </div>
                    <div className="flex justify-between gap-2">
                      <Button variant="outline" className="flex items-center gap-2">
                        <MessageCircle size={16} />
                        Message
                      </Button>
                      <Button className="flex items-center gap-2 bg-purple-600 hover:bg-purple-700">
                        <Heart size={16} />
                        J'aime
                      </Button>
                    </div>
                  </CardContent>
                </Card>
              ))}
            </div>
          </TabsContent>

          <TabsContent value="messages">
            <Card>
              <CardContent className="p-4">
                <h2 className="text-xl font-bold mb-4">Messages</h2>
                <p className="text-gray-500">
                  Fonctionnalité premium - Abonnez-vous pour accéder aux messages illimités
                </p>
                <Button className="mt-4 bg-purple-600 hover:bg-purple-700">
                  Voir les offres premium
                </Button>
              </CardContent>
            </Card>
          </TabsContent>

          <TabsContent value="likes">
            <Card>
              <CardContent className="p-4">
                <h2 className="text-xl font-bold mb-4">Qui vous a liké ?</h2>
                <p className="text-gray-500">
                  Fonctionnalité premium - Découvrez qui s'intéresse à votre profil
                </p>
                <Button className="mt-4 bg-purple-600 hover:bg-purple-700">
                  Débloquer cette fonction
                </Button>
              </CardContent>
            </Card>
          </TabsContent>

          <TabsContent value="profile">
            <Card>
              <CardContent className="p-4">
                <h2 className="text-xl font-bold mb-4">Mon Profil</h2>
                <div className="space-y-4">
                  <div>
                    <label className="block text-sm font-medium mb-1">Statut de vérification</label>
                    <div className="flex items-center gap-2 text-blue-500">
                      <Shield size={20} />
                      <span>Profil vérifié</span>
                    </div>
                  </div>
                  <div>
                    <label className="block text-sm font-medium mb-1">Abonnement</label>
                    <div className="flex items-center gap-2">
                      <Star size={20} className="text-yellow-500" />
                      <span>Premium</span>
                    </div>
                  </div>
                  <Button className="w-full bg-purple-600 hover:bg-purple-700">
                    Modifier mon profil
                  </Button>
                </div>
              </CardContent>
            </Card>
          </TabsContent>
        </Tabs>
      </div>

      <AIAssistant isOpen={isAIOpen} onClose={() => setIsAIOpen(false)} />
    </div>
  );
};

<a href="https://their-site.netlify.app/sub-
folder">Visitez ce site</a>
export default App;