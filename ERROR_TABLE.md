# Error table

# Error Handling Table

| Scenario | Detecting Function | Exact Error Value / Type | What the Player Sees |
| :--- | :--- | :--- | :--- |
| **Missing fleet file** | `data::load_fleet` | `std::io::Error` (NotFound) | `Error: could not load data/fleet.txt: ...` followed by program exit (`exit(1)`). |
| **Folder given as fleet path** | `data::load_fleet` | `std::io::Error` (IsADirectory) | `Error: could not load data/fleet.txt: ...` followed by program exit (`exit(1)`). |
| **Fleet file with only comments** | `data::load_fleet` | `DataError::NoShips` | `Error: could not load data/fleet.txt: ...` followed by program exit (`exit(1)`). |
| **Fleet file where every line is bad** | `data::load_fleet` | `Ok(FleetReport)` with populated `skipped` vec and empty `fleet` | Prints each skipped line (`data/fleet.txt line n: <message>`), then `No fleet loaded. Check data/fleet.txt.` and returns to menu. |
| **Board file with nine rows** | `data::load_board` | `DataError::InvalidBoard` | `Practice board unavailable: ...` |
| **Board file with a bad character** | `data::load_board` | `DataError::InvalidBoard` | `Practice board unavailable: ...` |
| **Missing scores file** | `data::load_scores` | `std::io::Error` (NotFound) handled internally as empty records | `scores unavailable: ...` (menu keeps running). |
| **Scores file that cannot be written** | `data::append_score` | `std::io::Error` | `Could not save the score: ...` (game continues). |
| **`K11` typed at prompt** | `board::parse_coord` | `CoordError::InvalidCoordinate` | Prints the exact error message from `CoordError`. |
