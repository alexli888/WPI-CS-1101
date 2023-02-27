# RacketDesign3
CS1101 Design3


; Design 3
(define WPI_ID1 "ajli") ; the text that comes before the @ in your wpi email
(define WPI_ID2 "mzheng"); fill in if working with a partner; leave as "" if working alone.

(require racket/base); added for UserIO implementation

;Design1 PART SECTION: Lines 6-97
;Design2 PART SECTION: Lines 102-282
;Design3 PART SECTION: Lines 294-358

; Description of Our Option Choices Design 3


; User IO Option Description: Interactive user input. User inputs info about the boat they
; entered, and at the end the program displays a text. The way to test is explained at the
; heading of the implementation.

; Abstraction Option Description: Function consumes a BST of Journeys and a predicate for each element
; produces true if all elements in the BST satisfy the predicate. Test by hitting run, Check-expects should pass.

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; Design1 START

; ; Part 1
; ;; The problem domain is:  sea travel
; ;; The category of things is: boats
; ;; The three sorts of  are: yacht, speedboat, sailboat
; ;; All three have the properties : can charter, know the location, has a captain
; ;; Yacht have the unique property: luxurious
; ;; Speedboat have the unique property: very fast
; ;; Sailboat have the unique property: eco friendly, comfy
; 
; ;; The types of computations we will do are:
; ;; 1) find the location of a boat
; 
; ;; 2) Determine which boat is most suitable for you
; ;; Yacht: luxurious, increases comfort, not eco feiendly
; ;; Speedboat: very fast, decreases comfort, not eco friendly
; ;; Sailboat: No fuel, increases comfort, eco friendly
; 

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;Part 2

(define-struct yacht (captain location))
;; a yacht is a (make-yacht captain string)
;interp.
;; The captain is the borowwer of the boat
;; Location is the place where the Yacht is docked
; ;; template:
; (define (yacht-fcn a-yacht)
;   (...
;    (yacht-captain a-yacht)
;    (yacht-location a-yacht)
;        )

;; examples:
(define DONALD-YACHT (make-yacht "Trump, Donald" "Monaco"))
(define JIANG-YACHT (make-yacht "Li, Jiang" "Shanghai"))


(define-struct speedboat (captain location))
;; a speedboat is a (make-speedboat captain string)
;interp.
;; The captain is the borowwer of the boat
;; Location is the place where the speedboat is docked
; ;; template:
; (define (speedboat-fcn a-speedboat)
;   (...
;    (speedboat-captain a-speedboat)
;    (speedboat-location a-speedboat)
;    )

;; examples:
(define KYLE-SPEEDBOAT (make-speedboat "Crash, Kyle" "Miami"))
(define KAREN-SPEEDBOAT (make-speedboat "Manager, Karen" "Tampa"))


(define-struct sailboat (captain location))
;; a sailboat is a (make-sailboat captain string)
;interp.
;; The captain is the borowwer of the boat
;; Location is the place where the sailboat is docked
; ;; template:
; (define (sailboat-fcn a-sailboat)
;   (...
;    (sailboat-captain a-sailboat)
;    (sailboat-location a-sailboat)
;        )

;; examples:
(define BRUCE-SAILBOAT (make-sailboat "Miller, Bruce P." "Bahamas"))
(define CHARLES-SAILBOAT (make-sailboat "Smith, Charles" "Australia"))

;; [TODO: Itemization Data Definition]
;; A Boat is the following:
;; -Yacht
;; -Speedboat
;; -Sailboat
;; interp. The three sorts of boats which our clients can borrow with info
;; about the boats

; ;; template:
; (define (boat-fcn a-boat)
;   (cond
;     [(Yacht? a-boat) (yacht-fcn a-boat)]
;     [(Speedboat? a-boat) (speedboat-fcn a-boat)]
;     [(Sailboat? a-boat) (sailboat-fcn a-boat)]
;     )
;   )



; Part 3

; Computation #1)
; ;; Step 1 - Signature, Purpose, Stub
; ;; Boat -> String
; ;; Purpose: consumes a boat then produces the location of that boat
; ;; stub:
; ;;(define (locate a-boat) "UK")


;; Step 2 - Examples(Tests)
(check-expect (locate DONALD-YACHT) "Monaco")
(check-expect (locate JIANG-YACHT) "Shanghai")
(check-expect (locate KYLE-SPEEDBOAT) "Miami")
(check-expect (locate CHARLES-SAILBOAT) "Australia")
(check-expect (locate BRUCE-SAILBOAT) "Bahamas")

; ;; Step 3 - Template and Inventory
; ;; template:
; ;(define (locate a-boat)
; ;  (cond
; ;    [(Yacht? a-boat) (yacht-fcn a-boat)]
; ;    [(Speedboat? a-boat) (speedboat-fcn a-boat)]
; ;    [(Sailboat? a-boat) (sailboat-fcn a-boat)]))
; ;inventory: I have selectors for each sort of boat, find boat location
; 

;; Step 4 - Function Body
(define (locate a-boat)
  (cond
    [(yacht? a-boat)     (yacht-location a-boat)]
    [(speedboat? a-boat) (speedboat-location a-boat)]
    [(sailboat? a-boat)  (sailboat-location a-boat)]
    )
  )

; Computation #2)
; ;; Step 1 - Signature, Purpose, Stub
; ;string->string
; 
; ; Purpose: consumes an adjective corresponding to each boat. Luxurious corresponds to yacht,
; ;fast corresponds to speedboat, comfy corresponds to sailboat, eco friendly corresponds to sailboat,
; ;price corresponds to "It depends on your personal preferences and priorities
; 
; ;Stub (define (suitable-boat criteria) "price")


;; Step 2 - Examples(Tests):
(check-expect (suitable-boat "luxurious") "yacht")
(check-expect (suitable-boat "fast") "speedboat")
(check-expect (suitable-boat "comfy") "sailboat")
(check-expect (suitable-boat "eco friendly") "sailboat")
(check-expect (suitable-boat "price") "Sorry, our boat rental company cannot assist you at this time, please try other services.")

; ;; Step 3 - Template and Inventory
; ;; template:
; ;(define (suitable-boat criteria)
; ;  (cond 
; ;    [(equal? criteria "CRITERIA_1") "yacht"]
; ;    [(equal? criteria "CRITERIA_2") "speedboat"]
; ;    [(equal? criteria "CRITERIA_3") "sailboat"]
; ;    [(equal? criteria "CRITERIA_4") "sailboat"]
; ;    [else "It depends on your personal preferences and priorities"]))
; 
; ;inventory: I have selectors for each sort of boat, outputs boat based on preference
; 


;; Step 4 - Function Body
(define (suitable-boat criteria)
  (cond 
    [(equal? criteria "luxurious") "yacht"]
    [(equal? criteria "fast") "speedboat"]
    [(equal? criteria "comfy") "sailboat"]
    [(equal? criteria "eco friendly") "sailboat"]
    [else "Sorry, our boat rental company cannot assist you at this time, please try other services."]
    )
  )
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;  Design 2 START


; Part 1: defined Compound Data, define List Type, Defined BST Type
; Defined Compound Data


(define-struct journey (boat new-captain miles destination))
; a Journey is a (make-journey (String String Natural String))
; interp. details about a journey
; - boat is the boat prior to rental
; - new-captain is the new captain renting the boat for a journey
; - miles is the number miles the journey took in total
; - location is where the journey ended

; Examples for Journey
(define Journey1 (make-journey KYLE-SPEEDBOAT "Duck" 500 "Alaska"))
(define Journey2 (make-journey DONALD-YACHT "Hillary" 800 "Sweden"))
(define Journey3 (make-journey BRUCE-SAILBOAT "Cat" 200 "Mexico"))

; Template for Journey
#;
(define (journey-fcn a-journey)
  (...
   (journey-boat a-journey)
   (journey-new-captain a-journey)
   (journey-miles a-journey)
   (journey-destination a-journey)))

; Defined List Type


; A ListOfBoat is one of:
; - empty
; - (cons Boat ListOfBoat)

; Examples
(define boats (cons "KYLE-SPEEDBOAT" (cons "DONALD-YACHT" (cons "BRUCE-SAILBOAT" empty))))

;Template:
#;
(define (lob-fnc a-lob)
  (cond [(empty? a-lob) ...]
        [(cons? a-lob)
           (...
              (boat-fcn (first a-lob))
              (lob-fcn (rest a-lob)))]))

; Defined BST Type


; A JourneyBST is one of
; - #false
; - (make-rnode Journey JourneyBST JourneyBST)

; INVARIANT:
;   left's Journey's miles < journey's mile's < right's journey's miles
(define-struct rnode (journey left right))
; KEY: miles 
; Interpretation: a BST of journey using miles traveled as the key for the BST


; Examples
(define RLEAF #false)
(define Journeys
   (make-rnode Journey2 ; 800mi                                
               (make-rnode Journey3 RLEAF RLEAF) ; 200mi    
                  (make-rnode Journey1 RLEAF RLEAF)))

;Visual Representation of JourneyBST:
;     800mi
;    /    \  
;  200mi 500mi
;  /  \   / \
; #f #f  #f #f

;Templates For the JourneyBST

; journey-bst-fcn : JourneyBST -> ...
#;
(define (journey-bst-fcn a-journey-bst)
  (cond
    [(false? a-journey-bst) ...]
    [(rnode? a-journey-bst)
     (...
      (journey-fcn (rnode-journey a-journey-bst))
      (journey-bst-fcn (rnode-left a-journey-bst))
      (journey-bst-fcn (rnode-right a-journey-bst)))]))

; journey-bst-search-fcn : JourneyBST Number -> ...
#;
(define (journey-bst-search-fcn a-journey-bst miles)
  (cond
    [(false? a-journey-bst) (... miles)]
    [(and
      (rnode? a-journey-bst)
      (= miles
         (journey-miles (rnode-journey a-journey-bst))))
     (journey-fcn (rnode-journey a-journey-bst))]
    [(and
      (rnode? a-journey-bst)
      (<  miles
          (journey-miles (rnode-journey a-journey-bst))))
      (journey-bst-search-fcn (rnode-left a-journey-bst))]
    [(and
      (rnode? a-journey-bst)
      (>  miles
          (journey-miles (rnode-journey a-journey-bst))))
      (journey-bst-search-fcn (rnode-right a-journey-bst))]))
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;PART 2 of Design2

;  Function that operates on Journey nested struct

; consumes the four inputs from the define struct ( boat, new-captain, miles, destination, target)
; The function adds a string "target" as the target destination.
; The function returns #t if the destination of the journey is equal to the target destination, and #f otherwise.
; is-destination-reached?: Journey -> Boolean

; TESTS
(check-expect (is-destination-reached? "KYLE-SPEEDBOAT" "Duck" 500 "Alaska" "Alaska") #t)
(check-expect (is-destination-reached? "DONALD-YACHT" "Hillary" 800 "Sweden" "Norway") #f)
(check-expect (is-destination-reached? "BRUCE-SAILBOAT" "Cat" 200 "Mexico" "Mexico") #t)
;TEMPLATE
; (define (is-destination-reached? boat new-captain miles destination target)
;   (... destination target ...))


;FUNCTION BODY
(define (is-destination-reached? boat new-captain miles destination target)
  (equal? destination target))
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;  Function that operates on ListOfBoat

; This function takes in a ListOfBoat, then outputs the number of boats in that list
; number-of-boats: ListOfBoats -> Number

; TESTS
(check-expect (number-of-boats (list KYLE-SPEEDBOAT)) 1)
(check-expect (number-of-boats (list KYLE-SPEEDBOAT DONALD-YACHT BRUCE-SAILBOAT)) 3)
(check-expect (number-of-boats '()) 0)

;TEMPLATE
; (define (number-of-boats a-list-of-boats)
;   (if (empty? a-list-of-boats)
;       ... ; fill in the result for an empty list
;       (+ 1 (number-of-boats (rest a-list-of-boats)))))


;FUNCTION BODY
(define (number-of-boats a-list-of-boats)
  (if (empty? a-list-of-boats)
      0
      (+ 1 (number-of-boats (rest a-list-of-boats)))))
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;  Function that operates on JourneyBST

; This function takes in a Journey miles, a range of miles, than outputs the boats that are inside that mile range.
; JourneyBST Number Number -> Vehicle or #false

; TESTS
(check-expect (boats-between-miles RLEAF 0 5000) #false)
(check-expect (boats-between-miles Journeys 0 5000) DONALD-YACHT)
(check-expect (boats-between-miles Journeys 2000 5000)#false)
(check-expect (boats-between-miles Journeys 0 10) #false)
(check-expect (boats-between-miles Journeys 100 2000) DONALD-YACHT)
(check-expect (boats-between-miles Journeys 0 500) BRUCE-SAILBOAT)
(check-expect (boats-between-miles Journeys 3000 4000) #f)
(check-expect (boats-between-miles Journeys 400 800) DONALD-YACHT)


; FUNCTION BODY
(define (boats-between-miles a-journey-bst low high)
  (cond
    [(false? a-journey-bst) #false]
 
    [(and 
      (rnode? a-journey-bst)
      (<= low
         (journey-miles (rnode-journey a-journey-bst)))
      (>= high
         (journey-miles (rnode-journey a-journey-bst))))
     (journey-boat (rnode-journey a-journey-bst))]
    
    [(and
      (rnode? a-journey-bst)
      (<  high
          (journey-miles (rnode-journey a-journey-bst))))
      (boats-between-miles (rnode-left a-journey-bst) low high)] 
    
    [(and
      (rnode? a-journey-bst)
      (>  low
          (journey-miles (rnode-journey a-journey-bst))))
      (boats-between-miles (rnode-right a-journey-bst) low high)]))
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; Design3 START

;  First Implementation: User IO

;; consumes nothing
;; produces a text after the user inputs the info about the boat they have rented
;; EFFECT: Prompts the user to input information

; ; How to Test : Input;  (define some-ride (user-journey!))
; into interaction area
; ; Then hit Enter and fill out the interaction boxes. Press Enter after filling each time.
; 
; ; Note the "error" else statement (the red text displayed) is just meant to be contrasting to the rest of the inputs
; ; Its not acually an error.
; 


(define (user-journey!)

  ; base cases 
  (local
    [(define a-string "")
     (define captain "") 
     (define miles 0)
     (define dest "")
     (define (starts-with c a-str) (string=? c (substring a-str 0 1)))
     (define (display-and-produce any) (begin (display any) any))] 
  
    ; user interaction begin 
    (begin
      (display "Which boat did you use???? Donalds, Kyle's Bruce's Jiang's")
      (set! a-string (string-downcase (read-line (current-input-port) 'any)))
      
      (display "Who was the captain of this boat?")
      (set! captain (read-line (current-input-port) 'any)) 
  
      (display "where did you go?")
      (set! dest (read-line (current-input-port) 'any)) 
       (make-journey
        (cond
          [(starts-with "D" a-string) DONALD-YACHT]
          [(starts-with "K" a-string) KYLE-SPEEDBOAT]
          [(starts-with "B" a-string) BRUCE-SAILBOAT]
          [(starts-with "J" a-string) JIANG-YACHT]
          [else (error "Yes, With your provided inputs The Boat that you have rented in our records shows to be the info you entered above.")])
        captain
        miles
        dest))))


; Second Implementation: Abstraction

;; andmap-bst : JourneyBST (P? -> Boolean) -> Boolean
;; consumes a BST of Journeys and a predicate for each element
;; produces true if all elements in the BST satisfy the predicate

;(define andmap-bst p? a-bst) #false)

(check-expect (andmap-bst empty? Journeys) #false)
(check-expect (andmap-bst number? Journeys) #false)

; ; Template
; ; bst-fcn : BST (... -> Boolean) -> Boolean 
; (define (bst-fcn a-bst)
;   (...
;     [(false? a-bst) ...]
;     [(rnode? a-bst)
;      (...
;       (... (rnode-journey a-bst))
;       (bst-fcn ... (rnode-left a-bst))
;       (bst-fcn ... (rnode-right a-bst))))]))


(define (andmap-bst p? a-bst) 
(cond
    [(false? a-bst) #true]
    [(rnode? a-bst)
     (and
      (p? (rnode-journey a-bst))
      (andmap-bst p? (rnode-left a-bst))
      (andmap-bst p? (rnode-right a-bst)))]))
