import React, { useState, useEffect } from 'react';
import {
  Search,
  MoreVertical,
  MessageSquare,
  Paperclip,
  Smile,
  Send,
  ChevronLeft,
  ChevronRight,
  User,
  Phone,
  Video,
  Menu,
} from 'lucide-react';
import { v4 as uuidv4 } from 'uuid';

// Mock data to simulate chats and messages
const initialChats = [
  {
    id: '1',
    name: 'Alice',
    lastMessage: 'Hey, how are you?',
    timestamp: '10:30 AM',
    avatarUrl: 'https://placehold.co/150x150/06B6D4/FFFFFF?text=A',
    messages: [
      { id: uuidv4(), text: 'Hey, how are you?', sender: 'Alice', timestamp: '10:30 AM' },
      { id: uuidv4(), text: 'I am good, thanks! How about you?', sender: 'Me', timestamp: '10:31 AM' },
    ],
  },
  {
    id: '2',
    name: 'Bob',
    lastMessage: 'See you tomorrow!',
    timestamp: 'Yesterday',
    avatarUrl: 'https://placehold.co/150x150/F97316/FFFFFF?text=B',
    messages: [
      { id: uuidv4(), text: 'Are we still on for tomorrow?', sender: 'Bob', timestamp: 'Yesterday' },
      { id: uuidv4(), text: 'Yes, looking forward to it!', sender: 'Me', timestamp: 'Yesterday' },
      { id: uuidv4(), text: 'See you tomorrow!', sender: 'Bob', timestamp: 'Yesterday' },
    ],
  },
  {
    id: '3',
    name: 'Charlie',
    lastMessage: 'Got it. Thanks!',
    timestamp: 'Monday',
    avatarUrl: 'https://placehold.co/150x150/EF4444/FFFFFF?text=C',
    messages: [
      { id: uuidv4(), text: 'Here is the document you asked for.', sender: 'Me', timestamp: 'Monday' },
      { id: uuidv4(), text: 'Got it. Thanks!', sender: 'Charlie', timestamp: 'Monday' },
    ],
  },
];

const App = () => {
  const [chats, setChats] = useState(initialChats);
  const [selectedChat, setSelectedChat] = useState(null);
  const [isMobile, setIsMobile] = useState(false);
  const [newMessage, setNewMessage] = useState('');

  // Handle window resize to manage mobile view state
  useEffect(() => {
    const handleResize = () => {
      setIsMobile(window.innerWidth < 768);
    };
    window.addEventListener('resize', handleResize);
    handleResize();
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  // Function to simulate sending a message
  const handleSendMessage = () => {
    if (newMessage.trim() === '' || !selectedChat) return;

    const newMsg = {
      id: uuidv4(),
      text: newMessage,
      sender: 'Me', // The current user
      timestamp: new Date().toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' }),
    };

    // Update the selected chat's messages and lastMessage
    const updatedChats = chats.map((chat) => {
      if (chat.id === selectedChat.id) {
        return {
          ...chat,
          messages: [...chat.messages, newMsg],
          lastMessage: newMsg.text,
          timestamp: newMsg.timestamp,
        };
      }
      return chat;
    });

    setChats(updatedChats);
    setSelectedChat(updatedChats.find(chat => chat.id === selectedChat.id));
    setNewMessage('');
  };

  const handleKeyDown = (e) => {
    if (e.key === 'Enter') {
      handleSendMessage();
    }
  };

  const ChatList = () => (
    <div className={`flex flex-col bg-slate-50 border-r border-slate-200 h-full ${isMobile && selectedChat ? 'hidden' : 'w-full md:w-1/3'}`}>
      <div className="flex items-center justify-between p-4 bg-slate-100 shadow-sm border-b border-slate-200">
        <div className="flex items-center">
          <div className="bg-cyan-500 rounded-full w-10 h-10 flex items-center justify-center font-bold text-white shadow-md mr-2">
            <User size={24} />
          </div>
          <span className="font-semibold text-lg text-slate-800">My Profile</span>
        </div>
        <div className="flex items-center space-x-3">
          <MessageSquare className="text-slate-600 hover:text-cyan-500 cursor-pointer transition-colors" />
          <MoreVertical className="text-slate-600 hover:text-cyan-500 cursor-pointer transition-colors" />
        </div>
      </div>
      <div className="p-3 bg-white border-b border-slate-200">
        <div className="relative">
          <Search className="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400" size={18} />
          <input
            type="text"
            placeholder="Search or start new chat"
            className="w-full pl-10 pr-4 py-2 rounded-lg bg-slate-100 focus:outline-none focus:ring-2 focus:ring-cyan-500 text-sm transition-all"
          />
        </div>
      </div>
      <div className="flex-1 overflow-y-auto custom-scrollbar">
        {chats.map((chat) => (
          <div
            key={chat.id}
            onClick={() => setSelectedChat(chat)}
            className={`flex items-center p-4 cursor-pointer border-b border-slate-200 transition-colors ${selectedChat && selectedChat.id === chat.id ? 'bg-cyan-100' : 'hover:bg-slate-100'}`}
          >
            <img
              src={chat.avatarUrl}
              alt={chat.name}
              className="w-12 h-12 rounded-full mr-4 object-cover border-2 border-white shadow-md"
            />
            <div className="flex-1">
              <h3 className="font-semibold text-slate-800">{chat.name}</h3>
              <p className="text-sm text-slate-500 truncate">{chat.lastMessage}</p>
            </div>
            <span className="text-xs text-slate-400 ml-2">{chat.timestamp}</span>
          </div>
        ))}
      </div>
    </div>
  );

  const MessageView = () => (
    <div className={`flex flex-col h-full bg-slate-100 ${isMobile && !selectedChat ? 'hidden' : 'w-full md:w-2/3'}`}>
      {selectedChat ? (
        <>
          <div className="flex items-center justify-between p-4 bg-slate-100 shadow-sm border-b border-slate-200">
            <div className="flex items-center">
              {isMobile && (
                <ChevronLeft
                  className="text-slate-600 mr-2 cursor-pointer md:hidden"
                  onClick={() => setSelectedChat(null)}
                />
              )}
              <img
                src={selectedChat.avatarUrl}
                alt={selectedChat.name}
                className="w-10 h-10 rounded-full mr-3 object-cover shadow-md"
              />
              <h2 className="font-semibold text-xl text-slate-800">{selectedChat.name}</h2>
            </div>
            <div className="flex items-center space-x-4">
              <Phone className="text-slate-600 hover:text-cyan-500 cursor-pointer transition-colors" />
              <Video className="text-slate-600 hover:text-cyan-500 cursor-pointer transition-colors" />
              <MoreVertical className="text-slate-600 hover:text-cyan-500 cursor-pointer transition-colors" />
            </div>
          </div>

          <div className="flex-1 p-6 overflow-y-auto custom-scrollbar">
            {selectedChat.messages.map((message, index) => (
              <div
                key={index}
                className={`flex mb-4 ${message.sender === 'Me' ? 'justify-end' : 'justify-start'}`}
              >
                <div
                  className={`max-w-xs lg:max-w-md p-3 rounded-xl shadow-lg relative ${
                    message.sender === 'Me'
                      ? 'bg-emerald-500 text-white rounded-br-none'
                      : 'bg-white text-slate-800 rounded-bl-none'
                  }`}
                >
                  <p className="text-sm">{message.text}</p>
                  <span className={`absolute bottom-1 text-xs ${message.sender === 'Me' ? 'text-white/70 right-3' : 'text-slate-400 right-2'}`}>{message.timestamp}</span>
                </div>
              </div>
            ))}
          </div>

          <div className="p-4 bg-slate-100 border-t border-slate-200">
            <div className="flex items-center space-x-3">
              <Smile className="text-slate-600 hover:text-cyan-500 cursor-pointer transition-colors" />
              <Paperclip className="text-slate-600 hover:text-cyan-500 cursor-pointer transition-colors" />
              <input
                type="text"
                value={newMessage}
                onChange={(e) => setNewMessage(e.target.value)}
                onKeyDown={handleKeyDown}
                placeholder="Type a message"
                className="flex-1 rounded-full py-3 px-5 bg-white border border-slate-200 focus:outline-none focus:ring-2 focus:ring-cyan-500 transition-all"
              />
              <button
                onClick={handleSendMessage}
                className="bg-cyan-500 text-white p-3 rounded-full shadow-lg hover:bg-cyan-600 focus:outline-none focus:ring-2 focus:ring-cyan-500 transition-colors"
              >
                <Send size={20} />
              </button>
            </div>
          </div>
        </>
      ) : (
        <div className="flex-1 flex flex-col items-center justify-center text-center p-6 bg-slate-50">
          <div className="max-w-md">
            <MessageSquare size={80} className="text-cyan-500 mx-auto mb-4" />
            <h1 className="text-3xl font-bold text-slate-800 mb-2">WhatsApp Clone</h1>
            <p className="text-slate-500 text-lg">
              Select a chat to start a conversation.
            </p>
          </div>
        </div>
      )}
    </div>
  );

  return (
    <div className="font-sans antialiased text-slate-800 bg-slate-100 min-h-screen flex flex-col">
      <style>{`
        .custom-scrollbar::-webkit-scrollbar {
          width: 8px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
          background-color: #cbd5e1;
          border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
          background-color: #94a3b8;
        }
      `}</style>
      <div className="flex flex-1 overflow-hidden">
        <ChatList />
        <MessageView />
      </div>
    </div>
  );
};

export default App;
