# OO 설계의 난관
이렇다 할 정답이 없음.  
사람처럼 생각하자는 것이 OOP. 즉 주관적임  
노트북을 하나의 개체로 볼 지 스크린, 키보드, 본체 세가지 개체의 조합으로 볼 지 다름.   
한 방에 제대로 설계하기도 힘듬.  

## 클래스 다이어그램 소개  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3553456c-e23e-4b97-96b9-5b7de4ab1ab2)  

(크게 구조를 보여주는 다이어그램 7개, 동작을 보여주는 다이어그램 7개 두 종류로 나뉨.)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/bc2f5ce7-1d22-423f-9f65-488769d0ad30)  
젤 위 : 클래스 이름.  
중간 : 멤버 변수.  
맨 밑 : 메서드.  

+기호 : public.  
-기호 : private.  
~기호 : default/package  

점선 화살표 : 의존관계  
A->B면 A가 B를 사용한다는 뜻.  

## 개체 모델링 팁
* 개체 모델링 시 모든 기능과 정보를 넣으려고 함
* 일단 작성한 코드는 유지보수의 대상.  
사용하지도 않는 멤버 변수, 메서드로 고치고 테스트 대상이라 유지보수 비용 증가.  
따라서 점진적으로 딱 필요한 것만 추가해야 함.  
보통 boolean형의 getter는 is를 많이 씀.  

두 클래스 개체가 상호작용하지 않음.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e9e0df55-d817-4af0-a988-dd374bfc48c3)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/bcba6db4-b05e-4eb9-be7c-10886119b398)  
방법1: 분무기를 화분에 대고 뿌린다.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6390ff85-672d-4325-8ebb-5350153226fa)  
훨씬 캡슐화, 추상화가 잘된 부분.  

방법2: 분무기를 줄 테니 알아서 뿌리세요 (?)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7adcdf55-944b-4676-b7f6-20292f738d55)  

둘 중에 뭐가 좋은가?  
1번이 뭔가 말이되고 2번이 좀 어색함. 그런데 2번에 더 객체지향적이고 장점이 존재함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/353d3d58-9a82-4225-92b9-d6b11f092c98)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/dadf6da0-5d05-428c-9662-d5e32a4dbbf1)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1a1786f8-4873-4620-a7ab-66269018fbbc)  

누군가의 질문 :  
1. 분무기.SprayTo(화분) : 화분줄테니 알아서 분무기님이 알아서 뿌리세요  
vs  
2. 화분.AddWater(분무기) : 분무기 줄테니 화분님이 알아서 뿌리세요  
Pope Kim's answer:  
상식(?) 상으로 생각하면 1번이 더 저희에게 자연스럽게 다가오는 건 사실입니다. 하지만 접근 권한(public/private 등)의 관점에서 생각한다면 1번은 화분에 물을 추가하는 public 함수가 생겨야겠죠. 그렇다면 분무기가 아닌 다른 것도 화분에 자유롭게 물을 줄 수가 있습니다.  

물을 아무나 자유로이 증가시키는 걸 막고 분무기만이 그렇게 할 수 있으려면 2번 방법을 택해야 한다는 거였죠.  

즉, 어느 관점에서 보느냐, 접근 제한이 필요하냐에 따라 이야기가 달라지는 부분... 복잡한 시스템일수록 자유로운 접근 제한 때문에 코드가 상호의존하여 유지보수가 어려워질 수도 있습니다. (의존성에 대해서는 뒤에 나옵니다)  

따라서 명확한 기준은 없다고 보셔도 됩니다. (...) 상식 vs 접근 제한 필요에 따라 잘 밸런스를 맞추는 수밖에요.  

머리와 몸통을 독자적인 개체로 인정하면?  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a2017baa-12a5-407e-b46c-9966338b6367)  

유연성 높은 설계가 최고다? ㄴㄴ  
재사용성이 많아지기는 하지만,  
클래스 수가 기하급수적으로 늘어날 수 있음.  
파일 이것저것 만들수록 어려워짐.  
유연성 높 : 성능 낮, 가독성 낮, 재사용성 높.  
필요에 따라서 유연성은 유연하게 조정할 것.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e53a3336-71ee-43ea-bad4-a3ff64ab353f)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4a8f35b3-6172-4daa-972f-fe2f615a8ced)  

대략의 크기를 enum으로 정해서 만든 코드.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8099796b-009b-40de-8c75-048e0ffa9328)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/bfbdd87e-2d63-43d4-8e5c-d50992c7200e)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7f120ad1-fda8-4777-b4c2-fae5c8814761)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/09622f01-fe3f-4866-8f14-dcf4b64c9d67)  

분무기를 직접 사용하기  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1147daeb-5a11-4d60-8c58-d27b8b5451e5)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/21a2a124-19b3-4cf6-aec3-733d09a93b56)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/24d95eb2-1b1b-44e0-80dd-69654eaf6d4c)  

code sample : PocuTunes.  
```java
// Song.java
package academu.pocu.comp2500samples.w03.pocutunes;

public class Song {
    private String artist;
    private String name;
    private int playTimeInMilliSeconds;
    
    public Song(String artist, String name, int playTimeInMilliSeconds) {
        this.artist = artist;
        this.name = name;
        this.playTimeInMilliSeconds = playTimeInMilliSeconds;
    }
    
    public String getArtist() {
        return this.artist;
    }
    
    public String getName() {
        return this.name;
    }
    
    public int getPlaytimeInMilliSeconds() {
        return this.playTimeInMilliSeconds;
    }
    
    public void play() {
        System.out.printf("Playing %s by %s. Duration is %d milliseconds%s",
                this.name,
                this.artist,
                this.playTimeInMilliSeconds,
                System.lineSeparator());
    }
}

// Playlist.java
package academy.pocu.comp2500samples.w03.pocutunes;

import java.util.ArrayList;

public class Playlist {
    private String name;
    private ArrayList<Song> songs;
    
    public PlayList(String name) {
        this.name = name;
        this.songs = new ArrayList<Song>();
    }
    
    public String getName() {
        return this.name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public void addSong(Song song) {
        this.songs.add(song);
    }
    
    public boolean removeSong(String songName) {
        Song song = findSongOrNull(songName);
        //TODO: this.findSongOrNull 안해도 되는건가? 왜그런건지 공부해야함
        
        if (song == null) {
            return false;
        }
        
        this.song.remove(song);
        return true;
    }
    
    public void play() {
        System.out.println(String.format("---Playing %s---", this.name));
    }
    
    private Song findSongOrNull(String songName) {
        for (Song song : this.songs) {
            if (songName.equals(song.getName())) {
                return song;
            }
        }
        
        return null;
    }
}

//PocuTunes.java
package academy.pocu.comp2500samples.w03.pocutunes;

import java.util.ArrayList;

public class PocuTunes {
    private ArrayList<Song> songs;
    private ArrayList<PlayList> playlists;
    
    public PocuTunes() {
        this(new ArrayList<Song>(), new ArrayList<PlayList>());
    }
    
    public PocuTunes(ArrayList<Song> songs, ArrayList<PlayList> playlists) {
        this.songs = songs;
        this.playlists = playlists;
    }
    
    public int getSongCount() {
        return this.songs.size();  //TODO: 얘는 ArrayList 내장함수인가?
    }
    
    public void addSong(Song song) {
        this.songs.add(song);
    }
    
    public boolean removeSong(String songName) {
        for (Playlist playlist : this.playlists) {  //TODO: 얘는 foreach문 비슷한건가?
            playlist.removeSong(songName);
        }
        
        Song songOrNull = findSongOrNull(songName);
        
        if (songOrNull == null) {
            return false;
        }
        
        this.songs.remove(songOrNull);
        return true;
    }
    
    public boolean removePlaylist(String playlistName) {
        for (Playlist playlist : this.playlists) {
            if (playlistName.equals(playlist.getName())) {
                this.playlists.remove(playlist);
                return true;
            }
        }
    }
    
    public void playSong(String songName) {
        Song songOrNull = findSongOrNull(songName);
        
        if (songOrNull == null) {
            System.out.println(String.format("\"%s\"not found!", songName));  // TODO: %s\ 는 왜한걸까?
            return;
        }
        
        songOrNull.play();
    }
    
    
    public void playPlaylist(String playlistName) {
        Playlist playlist = findPlaylistOrNull(playlistNmae);
        
        if (playlist == null) {
            System.out.println(String.format("Playlist %s not found!", playlistName));
            return;
        }
        
        playlist.play();
    }
    
    private Playlist findPlaylistOrNull(String playlistName) {
        for (Playlist playlist : this.playlists) {
            if (playlistNmae.equals(playlist.getName())) {
                return playlist;
            }
        }
        
        return null;
    }
    
    private Song findSongOrNull(String songName) {
        for (Song song : this.songs) {
            if (songName.equals(song.getName())) {
                return song;
            }
        }
        
        return null;
    }
}

//Program.java
package academy.pocu.comp2500samples.w03.pocutunes;

public class Program {
    public static void main(String[] args) {
        Song hotelCalifornia = new Song("Eagles",
                "Hotel California",
                180100); 

        Song heaven = new Song("Led Zeppelin",
                "Stairway to Heaven",
                172100);

        Song havana = new Song("Camila Cabello",
                "Havana",
                182200); 

        Song santaBaby = new Song("Ariana Grade",
                "Santa Baby",
                166220);

        Song houndDog = new Song("Elvis Presley",
                "Hound Dog",
                175220);

        Song basketCase = new Song("Green Day",
                "Basket Case",
                193000);

        Song christmas = new Song("Mariah Carey",
                "All I Want For Christmas Is You",
                18301);
                
        System.out.printf("%s by %s. Playtime is %d.%s",
                hotelCalifornia.getName(),
                hotelCalifornia.getArtist(),
                hotelCalifornia.getPlaytimeInMilliSeconds(),
                System.lineSeparator());
        
        Playlist playlist1 = new Playlist("Classic Rock");
        playlist1.addSong(hotelCalifornia);
        playlist1.addSong(heaven);
        playlist1.addSong(houndDog);

        Playlist playlist2 = new Playlist("Millenial");
        playlist2.addSong(havana);
        playlist2.addSong(santaBaby);

        PocuTunes tunes = new PocuTunes();
        
        tunes.addSong(hotelCalifornia);
        tunes.addSong(heaven);
        tunes.addSong(havana);
        tunes.addSong(santaBaby);
        tunes.addSong(houndDog);
        tunes.addSong(basketCase);
        tunes.addSong(christmas);

        System.out.printf("Song count %d%s",
                tunes.getSongCount(),
                System.lineSeparator());
                
        tunes.addPlaylist(playlist1);  //TODO: 중복 노래 검사는 안하나?
        tunes.addPlaylist(playlist2);

        tunes.playSong("Basket Case");
        tunes.playSong("Hound Dog");

        tunes.playSong("Escape");

        tunes.playPlaylist("Classic Rock");
        tunes.playPlaylist("Millenial");

        playlist2.setName("Christmas Music");
        playlist2.removeSong("Havana");
        playlist2.addSong(christmas);

        tunes.playPlaylist("Christmas Music");

        tunes.removeSong("Santa Baby");
        tunes.playPlaylist("Christmas Music");
        tunes.playSong("Santa Baby");

        tunes.removePlaylist("Christmas Music");

        System.out.printf("Song count %d.%s",
                tunes.getSongCount(),
                System.lineSeparator());
        tunes.playPlaylist("Christmas Music");
    }
}
```
