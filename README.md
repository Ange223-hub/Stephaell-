# Stephaell-
Site de rencontre amicaux au Burkina Faso
import React, { useState } from 'react';
import { Card, CardHeader, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Tabs, TabsList, TabsTrigger, TabsContent } from '@/components/ui/tabs';
import { MapPin, Heart, MessageCircle, Shield, Star } from 'lucide-react';

const App = () => {
  const [selectedCity, setSelectedCity] = useState('ouaga');
  const [activeTab, setActiveTab] = useState('explore');
  const [searchQuery, setSearchQuery] = useState('');

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
      verified: true
    },
    {
      id: 2,
      name: 'Marc O.',
      age: 28,
      city: 'Bobo-Dioulasso',
      interests: ['Musique', 'Voyage', 'Art'],
      verified: true
    }
  ];

  return (
    <div className="min-h-screen bg-gray-100 p-4">
      {/* Header */}
      <div className="max-w-4xl mx-auto bg-white rounded-lg shadow-md p-4 mb-4">
        <h1 className="text-2xl font-bold text-center text-purple-600 mb-4">
          Rencontres Amicales Burkina
        </h1>
        
        {/* City Selector */}
        <div className="flex items-center gap-2 mb-4">
          <MapPin className="text-gray-500" />
          <select 
            className="border rounded p-2"
            value={selectedCity}
            onChange={(e) => setSelectedCity(e.target.value)}
          >
            {cities.map(city => (
              <option key={city.id} value={city.id}>
                {city.name}
              </option>
            ))}
          </select>
        </div>

        {/* Search Bar */}
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

      {/* Main Content */}
      <div className="max-w-4xl mx-auto">
        <Tabs defaultValue="explore" className="w-full">
          <TabsList className="grid grid-cols-4 gap-4 mb-4">
            <TabsTrigger value="explore">Explorer</TabsTrigger>
            <TabsTrigger value="messages">Messages</TabsTrigger>
            <TabsTrigger value="likes">J'aime</TabsTrigger>
            <TabsTrigger value="profile">Profil</TabsTrigger>
          </TabsList>

          <TabsContent value="explore">
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              {profiles.map(profile => (
                <Card key={profile.id} className="w-full">
                  <CardHeader>
                    <div className="flex justify-between items-center">
                      <div>
                        <h3 className="font-bold">{profile.name}, {profile.age}</h3>
                        <p className="text-sm text-gray-500">
                          <MapPin className="inline-block mr-1" size={16} />
                          {profile.city}
                        </p>
                      </div>
                      {profile.verified && (
                        <Shield className="text-blue-500" size={20} />
                      )}
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
                    <div className="flex justify-between">
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
    </div>
  );
};

export default App;
