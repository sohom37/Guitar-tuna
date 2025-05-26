# Guitar-tuna
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.6
  http: ^1.2.1 # For future API calls if you have a backend
 class Song {
  final String id;
  final String title;
  final String artist;
  final String tabContent; // Basic text tab

  Song({
    required this.id,
    required this.title,
    required this.artist,
    required this.tabContent,
  });

  // Example of how you might create a Song from JSON data
  factory Song.fromJson(Map<String, dynamic> json) {
    return Song(
      id: json['id'],
      title: json['title'],
      artist: json['artist'],
      tabContent: json['tabContent'],
    );
  }
} 
  import 'package:flutter/material.dart';
import 'package:guitar_learning_app/models/song.dart';
import 'package:guitar_learning_app/screens/song_detail_screen.dart';

class SongListScreen extends StatefulWidget {
  const SongListScreen({super.key});

  @override
  State<SongListScreen> createState() => _SongListScreenState();
}

class _SongListScreenState extends State<SongListScreen> {
  // Dummy data for demonstration. In a real app, this would come from an API.
  final List<Song> _songs = [
    Song(
      id: 's1',
      title: 'Stairway to Heaven',
      artist: 'Led Zeppelin',
      tabContent: '''
(Intro)
Am G C F
e|--------------0-------------------------|
B|------------1----1----------------------|
G|----------2--------2--------------------|
D|--------2------------2------------------|
A|------0---------------------------------|
E|----------------------------------------|
(Verse 1)
There's a lady who's sure all that glitters is gold
And she's buying a stairway to heaven.
When she gets there she knows, if the stores are all closed
With a word she can get what she came for.
... (more tab content)
''',
    ),
    Song(
      id: 's2',
      title: 'Smoke on the Water',
      artist: 'Deep Purple',
      tabContent: '''
(Main Riff)
e|-----------------|
B|-----------------|
G|-----------------|
D|--0--3--5---0--3--6--5--|
A|--0--3--5---0--3--6--5--|
E|-----------------|
... (more tab content)
''',
    ),
    // Add more songs here
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Guitar Tabs'),
        actions: [
          IconButton(
            icon: const Icon(Icons.search),
            onPressed: () {
              // Implement search functionality here
            },
          ),
        ],
      ),
      body: ListView.builder(
        itemCount: _songs.length,
        itemBuilder: (context, index) {
          final song = _songs[index];
          return Card(
            margin: const EdgeInsets.symmetric(horizontal: 10, vertical: 5),
            child: ListTile(
              title: Text(song.title),
              subtitle: Text(song.artist),
              onTap: () {
                Navigator.of(context).push(
                  MaterialPageRoute(
                    builder: (context) => SongDetailScreen(song: song),
                  ),
                );
              },
            ),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Implement add new song functionality
          // (e.g., navigate to a screen for user to upload tab)
        },
        child: const Icon(Icons.add),
      ),
    );
  }
}
import 'package:flutter/material.dart';
import 'package:guitar_learning_app/models/song.dart';
import 'package:guitar_learning_app/screens/song_detail_screen.dart';

class SongListScreen extends StatefulWidget {
  const SongListScreen({super.key});

  @override
  State<SongListScreen> createState() => _SongListScreenState();
}

class _SongListScreenState extends State<SongListScreen> {
  // Dummy data for demonstration. In a real app, this would come from an API.
  final List<Song> _songs = [
    Song(
      id: 's1',
      title: 'Stairway to Heaven',
      artist: 'Led Zeppelin',
      tabContent: '''
(Intro)
Am G C F
e|--------------0-------------------------|
B|------------1----1----------------------|
G|----------2--------2--------------------|
D|--------2------------2------------------|
A|------0---------------------------------|
E|----------------------------------------|
(Verse 1)
There's a lady who's sure all that glitters is gold
And she's buying a stairway to heaven.
When she gets there she knows, if the stores are all closed
With a word she can get what she came for.
... (more tab content)
''',
    ),
    Song(
      id: 's2',
      title: 'Smoke on the Water',
      artist: 'Deep Purple',
      tabContent: '''
(Main Riff)
e|-----------------|
B|-----------------|
G|-----------------|
D|--0--3--5---0--3--6--5--|
A|--0--3--5---0--3--6--5--|
E|-----------------|
... (more tab content)
''',
    ),
    // Add more songs here
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Guitar Tabs'),
        actions: [
          IconButton(
            icon: const Icon(Icons.search),
            onPressed: () {
              // Implement search functionality here
            },
          ),
        ],
      ),
      body: ListView.builder(
        itemCount: _songs.length,
        itemBuilder: (context, index) {
          final song = _songs[index];
          return Card(
            margin: const EdgeInsets.symmetric(horizontal: 10, vertical: 5),
            child: ListTile(
              title: Text(song.title),
              subtitle: Text(song.artist),
              onTap: () {
                Navigator.of(context).push(
                  MaterialPageRoute(
                    builder: (context) => SongDetailScreen(song: song),
                  ),
                );
              },
            ),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Implement add new song functionality
          // (e.g., navigate to a screen for user to upload tab)
        },
        child: const Icon(Icons.add),
      ),
    );
  }
}

import 'package:flutter/material.dart';
import 'package:guitar_learning_app/models/song.dart';

class SongDetailScreen extends StatelessWidget {
  final Song song;

  const SongDetailScreen({super.key, required this.song});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('${song.title} by ${song.artist}'),
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              song.title,
              style: const TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 8),
            Text(
              song.artist,
              style: const TextStyle(fontSize: 18, fontStyle: FontStyle.italic),
            ),
            const SizedBox(height: 20),
            // Displaying the tab content.
            // For better formatting, you might need a custom renderer
            // or a package that handles preformatted text.
            Container(
              decoration: BoxDecoration(
                color: Colors.grey[900],
                borderRadius: BorderRadius.circular(8),
              ),
              padding: const EdgeInsets.all(12),
              child: SelectableText( // Allows text selection for copying
                song.tabContent,
                style: const TextStyle(
                  fontFamily: 'monospace', // Essential for tabs to align
                  fontSize: 14,
                  color: Colors.white,
                ),
              ),
            ),
            const SizedBox(height: 20),
            // TODO: Add learning tools here (metronome, looping, chord diagrams)
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceAround,
              children: [
                ElevatedButton.icon(
                  onPressed: () {
                    // Implement metronome/tempo control
                  },
                  icon: const Icon(Icons.speed),
                  label: const Text('Tempo'),
                ),
                ElevatedButton.icon(
                  onPressed: () {
                    // Implement looping
                  },
                  icon: const Icon(Icons.loop),
                  label: const Text('Loop'),
                ),
                ElevatedButton.icon(
                  onPressed: () {
                    // Implement chord dictionary
                  },
                  icon: const Icon(Icons.music_note),
                  label: const Text('Chords'),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
import 'package:flutter/material.dart';
import 'package:guitar_learning_app/screens/song_list_screen.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Free Guitar Learning',
      theme: ThemeData(
        primarySwatch: Colors.blueGrey,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: const SongListScreen(),
    );
  }
}
