# Very Best Debug

  - Transcription `very-best-debug-video.md` contains time-stamped sections matching the headings here

  - Chapters (and slides):

  - Workspace open, tabs organized, aware of /git committing and rails grade. Link to technical setup.

### Video Segment: Homepage Debugging (da="Tutorial")

  - RTEM to slowly debug **/**
  - `better_errors` page console aside (da="Explain")
  
#### Text Companion: Homepage Debugging (da="HowTo")

### Video Segment: Typos and `NilClass` Bug (da="Tutorial")

  - RTEM to slowly debug **/venues/[ID of venue]**
  - tricky bug: `undefined method 'address' for nil:NilClass` 
  - `ActiveRecord::Relation` single instance `.at(0)`
  
#### Text Companion: Typos and `NilClass` Bug (da="HowTo")

### Video Segment: Association Accessor `self.id` Bug (da="Tutorial")

  - RTEM to continue debugging **/venues/[ID of venue]**
  - tricky bug: `self.id` in `Comment#commenter`, rather than `self.author_id` 
  
#### Text Companion: Association Accessor `self.id` Bug (da="HowTo")

### Finish and Submit Very Best Debug (da="Exercise")

  - see list from README: https://github.com/appdev-projects/very-best-debug#readme
