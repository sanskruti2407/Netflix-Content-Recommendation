# Netflix-Content-Recommendation
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAX_CONTENT 20
#define MAX_GENRE_LENGTH 30

// Structure to represent a Netflix content item (movie or TV show)
typedef struct {
    char title[50];
    char genre[MAX_GENRE_LENGTH];
    float rating;
    char spoiler[100]; // Added spoiler field
} Content;

// Recursive function to suggest content based on genre
void suggestContentByGenre(Content contentList[MAX_CONTENT], int index, const char* preferredGenre) {
    // Base case: If we've checked all the content, return
    if (index == MAX_CONTENT) {
        return;
    }

    // If the genre matches, print the title, rating, and spoiler
    if (strcasecmp(contentList[index].genre, preferredGenre) == 0) {
        printf("Recommended: %s (Genre: %s, Rating: %.1f)\n", contentList[index].title, contentList[index].genre, contentList[index].rating);
        printf("Spoiler: %s\n\n", contentList[index].spoiler);
    }

    // Recur to the next content item
    suggestContentByGenre(contentList, index + 1, preferredGenre);
}

int main() {
    // Sample Netflix content list with spoilers
    Content contentList[MAX_CONTENT] = {
        {"Inception", "Sci-Fi", 8.8, "A dream within a dream - layers of reality blur as Cobb tries to return home."},
        {"The Matrix", "Sci-Fi", 8.7, "Neo discovers he is 'The One' destined to free humanity from a simulation."},
        {"Friends", "Comedy", 8.9, "Six friends navigate life, love, and hilarity in New York City."},
        {"Breaking Bad", "Drama", 9.5, "Walter White becomes a feared drug kingpin to secure his family's future."},
        {"Stranger Things", "Sci-Fi", 8.7, "A young boy disappears, revealing a secret dimension called the Upside Down."},
        {"The Office", "Comedy", 8.8, "Michael Scott's antics at Dunder Mifflin create chaos and laughter."},
        {"The Dark Knight", "Action", 9.0, "Batman faces off against the Joker, a criminal mastermind causing chaos."},
        {"The Crown", "Drama", 8.7, "The life of Queen Elizabeth II and the challenges of the British monarchy."},
        {"The Witcher", "Fantasy", 8.2, "Geralt of Rivia battles monsters and destiny in a world of chaos."},
        {"Narcos", "Crime", 8.8, "The rise and fall of Pablo Escobar and the Medellín cartel."},
        {"Money Heist", "Crime", 8.2, "The Professor masterminds a thrilling heist with unexpected twists."},
        {"Mismatch", "Romcom", 8.9, "An unlikely couple learns love and understanding through awkward moments."},
        {"The Vampire Diaries", "Suspense", 9.0, "A centuries-old love triangle leads to danger and heartbreak."},
        {"Yeh Jawaani Hai Deewani", "Friendship", 8.7, "A journey of self-discovery and friendship during an adventurous trip."}
    };

    // Ask the user for their preferred genre
    char preferredGenre[MAX_GENRE_LENGTH];
    printf("Enter your preferred genre (e.g., Sci-Fi, Comedy, Drama, Romcom, Suspense, Friendship, Fantasy, Crime, Action): ");
    scanf("%s", preferredGenre);

    printf("\n--- Content Suggestions ---\n");
    // Start the recursive search from the first content item
    suggestContentByGenre(contentList, 0, preferredGenre);

    return 0;
}
