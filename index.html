import React, { useState, useEffect, useRef } from 'react';
import { Send, Users, MessageCircle } from 'lucide-react';

export default function ChatRoom() {
  const [username, setUsername] = useState('');
  const [isJoined, setIsJoined] = useState(false);
  const [messages, setMessages] = useState([]);
  const [newMessage, setNewMessage] = useState('');
  const [onlineUsers, setOnlineUsers] = useState([]);
  const messagesEndRef = useRef(null);

  const scrollToBottom = () => {
    messagesEndRef.current?.scrollIntoView({ behavior: 'smooth' });
  };

  useEffect(() => {
    scrollToBottom();
  }, [messages]);

  useEffect(() => {
    if (isJoined) {
      loadMessages();
      loadUsers();
      
      const interval = setInterval(() => {
        loadMessages();
        loadUsers();
      }, 2000);

      return () => clearInterval(interval);
    }
  }, [isJoined]);

  const loadMessages = async () => {
    try {
      const result = await window.storage.list('msg:', true);
      if (result && result.keys) {
        const messagePromises = result.keys.map(async (key) => {
          const data = await window.storage.get(key, true);
          return data ? JSON.parse(data.value) : null;
        });
        
        const loadedMessages = (await Promise.all(messagePromises))
          .filter(m => m !== null)
          .sort((a, b) => a.timestamp - b.timestamp);
        
        setMessages(loadedMessages);
      }
    } catch (error) {
      console.log('Loading messages...');
    }
  };

  const loadUsers = async () => {
    try {
      const result = await window.storage.list('user:', true);
      if (result && result.keys) {
        const userPromises = result.keys.map(async (key) => {
          const data = await window.storage.get(key, true);
          if (!data) return null;
          const user = JSON.parse(data.value);
          if (Date.now() - user.lastSeen < 10000) {
            return user.username;
          }
          return null;
        });
        
        const users = (await Promise.all(userPromises)).filter(u => u !== null);
        setOnlineUsers(users);
      }
    } catch (error) {
      console.log('Loading users...');
    }
  };

  const updatePresence = async () => {
    if (!username) return;
    try {
      await window.storage.set(
        `user:${username}`,
        JSON.stringify({ username, lastSeen: Date.now() }),
        true
      );
    } catch (error) {
      console.log('Updating presence...');
    }
  };

  useEffect(() => {
    if (isJoined) {
      updatePresence();
      const presenceInterval = setInterval(updatePresence, 5000);
      return () => clearInterval(presenceInterval);
    }
  }, [isJoined, username]);

  const handleJoin = () => {
    if (username.trim()) {
      setIsJoined(true);
      updatePresence();
    }
  };

  const handleSendMessage = async () => {
    if (newMessage.trim() && username) {
      const message = {
        id: `${Date.now()}-${Math.random()}`,
        username,
        text: newMessage.trim(),
        timestamp: Date.now()
      };

      try {
        await window.storage.set(`msg:${message.id}`, JSON.stringify(message), true);
        setNewMessage('');
        loadMessages();
      } catch (error) {
        console.error('Failed to send message');
      }
    }
  };

  const handleKeyPress = (e) => {
    if (e.key === 'Enter' && !e.shiftKey) {
      e.preventDefault();
      if (isJoined) {
        handleSendMessage();
      } else {
        handleJoin();
      }
    }
  };

  const formatTime = (timestamp) => {
    const date = new Date(timestamp);
    return date.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' });
  };

  if (!isJoined) {
    return (
      <div className="min-h-screen bg-gradient-to-br from-blue-500 to-purple-600 flex items-center justify-center p-4">
        <div className="bg-white rounded-2xl shadow-2xl p-8 w-full max-w-md">
          <div className="flex justify-center mb-6">
            <div className="bg-gradient-to-br from-blue-500 to-purple-600 p-4 rounded-full">
              <MessageCircle className="w-12 h-12 text-white" />
            </div>
          </div>
          <h1 className="text-3xl font-bold text-center mb-2 text-gray-800">
            Welcome to ChatRoom
          </h1>
          <p className="text-center text-gray-600 mb-8">
            Enter your name to join the conversation
          </p>
          <div>
            <input
              type="text"
              placeholder="Enter your username"
              value={username}
              onChange={(e) => setUsername(e.target.value)}
              onKeyPress={handleKeyPress}
              className="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:outline-none focus:border-blue-500 mb-4"
              maxLength={20}
            />
            <button
              onClick={handleJoin}
              className="w-full bg-gradient-to-r from-blue-500 to-purple-600 text-white py-3 rounded-lg font-semibold hover:shadow-lg transition-shadow"
            >
              Join Chat Room
            </button>
          </div>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gray-100 flex">
      <div className="w-64 bg-white shadow-lg p-4 hidden md:block">
        <div className="flex items-center gap-2 mb-6 pb-4 border-b">
          <Users className="w-6 h-6 text-blue-500" />
          <h2 className="font-bold text-lg">Online Users ({onlineUsers.length})</h2>
        </div>
        <div className="space-y-2">
          {onlineUsers.map((user, idx) => (
            <div key={idx} className="flex items-center gap-2 p-2 rounded hover:bg-gray-50">
              <div className="w-2 h-2 bg-green-500 rounded-full"></div>
              <span className={`text-sm ${user === username ? 'font-bold text-blue-600' : 'text-gray-700'}`}>
                {user} {user === username && '(You)'}
              </span>
            </div>
          ))}
        </div>
      </div>

      <div className="flex-1 flex flex-col">
        <div className="bg-white shadow-sm p-4 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <MessageCircle className="w-6 h-6 text-blue-500" />
            <div>
              <h1 className="text-xl font-bold text-gray-800">ChatRoom</h1>
              <p className="text-sm text-gray-500">Logged in as {username}</p>
            </div>
          </div>
          <div className="flex items-center gap-2 text-sm text-gray-600 md:hidden">
            <Users className="w-4 h-4" />
            <span>{onlineUsers.length} online</span>
          </div>
        </div>

        <div className="flex-1 overflow-y-auto p-4 space-y-4">
          {messages.length === 0 ? (
            <div className="text-center text-gray-400 mt-20">
              <MessageCircle className="w-16 h-16 mx-auto mb-4 opacity-50" />
              <p>No messages yet. Start the conversation!</p>
            </div>
          ) : (
            messages.map((msg) => (
              <div
                key={msg.id}
                className={`flex ${msg.username === username ? 'justify-end' : 'justify-start'}`}
              >
                <div
                  className={`max-w-xs lg:max-w-md px-4 py-2 rounded-2xl ${
                    msg.username === username
                      ? 'bg-gradient-to-r from-blue-500 to-purple-600 text-white'
                      : 'bg-white shadow'
                  }`}
                >
                  <div className="flex items-baseline gap-2 mb-1">
                    <span
                      className={`text-xs font-semibold ${
                        msg.username === username ? 'text-blue-100' : 'text-blue-600'
                      }`}
                    >
                      {msg.username}
                    </span>
                    <span
                      className={`text-xs ${
                        msg.username === username ? 'text-blue-100' : 'text-gray-500'
                      }`}
                    >
                      {formatTime(msg.timestamp)}
                    </span>
                  </div>
                  <p className="break-words">{msg.text}</p>
                </div>
              </div>
            ))
          )}
          <div ref={messagesEndRef} />
        </div>

        <div className="bg-white border-t p-4">
          <div className="flex gap-2">
            <input
              type="text"
              placeholder="Type a message..."
              value={newMessage}
              onChange={(e) => setNewMessage(e.target.value)}
              onKeyPress={handleKeyPress}
              className="flex-1 px-4 py-3 border border-gray-300 rounded-full focus:outline-none focus:border-blue-500"
              maxLength={500}
            />
            <button
              onClick={handleSendMessage}
              className="bg-gradient-to-r from-blue-500 to-purple-600 text-white p-3 rounded-full hover:shadow-lg transition-shadow"
            >
              <Send className="w-5 h-5" />
            </button>
          </div>
        </div>
      </div>
    </div>
  );
}
