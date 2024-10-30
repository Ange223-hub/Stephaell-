import React, { useState } from 'react';
import { User, Search, MessageCircle, Home, MapPin, Shield, Coffee, Heart, Users } from 'lucide-react';
import { Card, CardHeader, CardContent } from '@/components/ui/card';

const BurkinaConnect = () => {
  const [activeTab, setActiveTab] = useState('home');
  const [activeCategory, setActiveCategory] = useState('amitié');

  const profiles = [
    {
      name: "Aminata",
      age: 25,
      ville: "Ouagadougou",
      intérêts: ["Culture", "Sport", "Lecture"],
      recherche: "Amitié",
      verified: true
    },
    {
      name: "Ibrahim",
      age: 28,
      ville: "Bobo-Dioulasso",
      intérêts: ["Musique", "Voyages", "Cuisine"],
      recherche: "Relation sérieuse",
      verified: true
    },
    {
      name: "Fatima",
      age: 23,
      ville: "Koudougou",
      intérêts: ["Art", "Cinéma", "Bénévolat"],
      recherche: "Sorties",
      verified: true
    }
  ];

  const renderContent = () => {
    switch(activeTab) {
      case 'home':
        return (
          <div className="space-y-4 p-4">
            <div className="bg-green-100 p-4 rounded-lg mb-6">
              <h2 className="text-xl font-bold mb-2">Burkina Connect</h2>
              <p className="text-gray-600">Rencontrez de nouvelles personnes en toute sécurité</p>
            </div>
            
            <div className="flex gap-4 overflow-x-auto pb-2">
              <button 
                className={`px-4 py-2 rounded-full whitespace-nowrap ${
                  activeCategory === 'amitié' ? 'bg-green-500 text-white' : 'bg-green-100'
                }`}
                onClick={() => setActiveCategory('amitié')}
              >
                <div className="flex items-center gap-2">
                  <Users size={16} />
                  <span>Amitié</span>
                </div>
              </button>
              <button 
                className={`px-4 py-2 rounded-full whitespace-nowrap ${
                  activeCategory === 'sorties' ? 'bg-green-500 text-white' : 'bg-green-100'
                }`}
                onClick={() => setActiveCategory('sorties')}
              >
                <div className="flex items-center gap-2">
                  <Coffee size={16} />
                  <span>Sorties</span>
                </div>
              </button>
              <button 
                className={`px-4 py-2 rounded-full whitespace-nowrap ${
                  activeCategory === 'sérieux' ? 'bg-green-500 text-white' : 'bg-green-100'
                }`}
                onClick={() => setActiveCategory('sérieux')}
              >
                <div className="flex items-center gap-2">
                  <Heart size={16} />
                  <span>Relation sérieuse</span>
                </div>
              </button>
            </div>

            <div className="space-y-4">
              {profiles.map((profile, index) => (
                <Card key={index} className="w-full">
                  <CardContent className="p-4">
                    <div className="flex items-start gap-4">
                      <div className="w-16 h-16 bg-gray-200 rounded-full flex items-center justify-center">
                        <User size={32} className="text-gray-500" />
                      </div>
                      <div className="flex-1">
                        <div className="flex justify-between items-start">
                          <div>
                            <div className="flex items-center gap-2">
                              <h3 className="font-semibold">{profile.name}, {profile.age}</h3>
                              {profile.verified && (
                                <Shield size={16} className="text-green-500" />
                              )}
                            </div>
                            <p className="text-sm text-gray-600 flex items-center gap-1">
                              <MapPin size={14} />
                              {profile.ville}
                            </p>
                          </div>
                        </div>
                        <div className="mt-2">
                          <p className="text-sm text-gray-600">Recherche: {profile.recherche}</p>
                          <div className="flex flex-wrap gap-2 mt-2">
                            {profile.intérêts.map((intérêt, i) => (
                              <span key={i} className="text-xs bg-gray-100 px-2 py-1 rounded">
                                {intérêt}
                              </span>
                            ))}
                          </div>
                        </div>
                      </div>
                    </div>
                  </CardContent>
                </Card>
              ))}
            </div>
          </div>
        );
      
      case 'search':
        return (
          <div className="p-4">
            <div className="relative mb-4">
              <input
                type="text"
                placeholder="Rechercher des personnes..."
                className="w-full p-3 border rounded-lg pl-10"
              />
              <Search className="absolute left-3 top-3 text-gray-400" size={20} />
            </div>
            <div className="space-y-4">
              <h3 className="font-semibold">Filtres</h3>
              <div className="grid grid-cols-2 gap-2">
                <button className="p-2 border rounded">Ville</button>
                <button className="p-2 border rounded">Âge</button>
                <button className="p-2 border rounded">Intérêts</button>
                <button className="p-2 border rounded">Type de rencontre</button>
              </div>
            </div>
          </div>
        );

      case 'subscription':
        return (
          <div className="p-4">
            <h2 className="text-xl font-bold mb-4">Abonnement Premium</h2>
            <Card className="mb-4">
              <CardContent className="p-4">
                <h3 className="font-semibold mb-2">Avantages Premium</h3>
                <ul className="space-y-2">
                  <li className="flex items-center gap-2">
                    <Shield size={16} className="text-green-500" />
                    <span>Profil vérifié</span>
                  </li>
                  <li className="flex items-center gap-2">
                    <MessageCircle size={16} className="text-green-500" />
                    <span>Messages illimités</span>
                  </li>
                  <li className="flex items-center gap-2">
                    <Users size={16} className="text-green-500" />
                    <span>Voir qui vous a liké</span>
                  </li>
                </ul>
              </CardContent>
            </Card>

            <Card className="mb-4">
              <CardContent className="p-4">
                <h3 className="font-semibold mb-2">Paiement par Orange Money</h3>
                <p className="text-sm text-gray-600 mb-4">Numéro: +226 66798031</p>
                <div className="space-y-2">
                  <button className="w-full p-3 bg-orange-500 text-white rounded-lg">
                    1 mois - 2000 FCFA
                  </button>
                  <button className="w-full p-3 bg-orange-500 text-white rounded-lg">
                    3 mois - 5000 FCFA
                  </button>
                  <button className="w-full p-3 bg-orange-500 text-white rounded-lg">
                    6 mois - 9000 FCFA
                  </button>
                </div>
              </CardContent>
            </Card>
          </div>
        );

      case 'profile':
        return (
          <div className="p-4">
            <div className="text-center mb-6">
              <div className="w-24 h-24 bg-gray-200 rounded-full mx-auto mb-4 flex items-center justify-center">
                <User size={40} className="text-gray-500" />
              </div>
              <h2 className="text-xl font-bold">Mon Profil</h2>
            </div>
            <div className="space-y-4">
              <button className="w-full p-3 border rounded-lg text-left">
                Modifier mon profil
              </button>
              <button className="w-full p-3 border rounded-lg text-left">
                Paramètres de confidentialité
              </button>
              <button className="w-full p-3 border rounded-lg text-left">
                Vérification du profil
              </button>
              <button className="w-full p-3 border rounded-lg text-left text-red-500">
                Déconnexion
              </button>
            </div>
          </div>
        );
      default:
        return null;
    }
  };

  return (
    <div className="w-full max-w-md mx-auto h-[600px] bg-white rounded-xl shadow-lg overflow-hidden flex flex-col">
      <div className="bg-green-500 text-white p-4">
        <h1 className="text-xl font-bold">Burkina Connect</h1>
      </div>
      
      <div className="flex-1 overflow-y-auto">
        {renderContent()}
      </div>
      
      <div className="border-t bg-white">
        <div className="flex justify-around p-3">
          <button
            onClick={() => setActiveTab('home')}
            className={`flex flex-col items-center ${activeTab === 'home' ? 'text-green-500' : 'text-gray-500'}`}
          >
            <Home size={24} />
            <span className="text-xs mt-1">Accueil</span>
          </button>
          <button
            onClick={() => setActiveTab('search')}
            className={`flex flex-col items-center ${activeTab === 'search' ? 'text-green-500' : 'text-gray-500'}`}
          >
            <Search size={24} />
            <span className="text-xs mt-1">Recherche</span>
          </button>
          <button
            onClick={() => setActiveTab('subscription')}
            className={`flex flex-col items-center ${activeTab === 'subscription' ? 'text-green-500' : 'text-gray-500'}`}
          >
            <Shield size={24} />
            <span className="text-xs mt-1">Premium</span>
          </button>
          <button
            onClick={() => setActiveTab('profile')}
            className={`flex flex-col items-center ${activeTab === 'profile' ? 'text-green-500' : 'text-gray-500'}`}
          >
            <User size={24} />
            <span className="text-xs mt-1">Profil</span>
          </button>
        </div>
      </div>
    </div>
  );
};

export default BurkinaConnect;
