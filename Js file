let boxes = document.querySelectorAll(".box");
let resetBtn = document.querySelector("#reset-btn");
let newgamebtn = document.querySelector("#new-btn");
let undoBtn = document.querySelector("#undo-btn");
let redoBtn = document.querySelector("#redo-btn");
let msgContainer = document.querySelector(".msg-container");
let msg = document.querySelector("#msg");

let turn0 = true;
let moveHistory = [];
let redoHistory = [];

const winpattern = [
    [0,1,2],
    [0,3,6],
    [3,4,5],
    [6,7,8],
    [0,4,8],
    [1,4,7],
    [2,5,8],
    [2,4,6],
    
];

const resetGame = () => {
    turn0 = true;
    moveHistory = [];
    redoHistory = [];
    enableBoxes();
    msgContainer.classList.add("hide");
    updateUndoRedoButtons();
};

const updateUndoRedoButtons = () => {
    undoBtn.disabled = moveHistory.length === 0;
    redoBtn.disabled = redoHistory.length === 0;
};

boxes.forEach((box, index) => {
    box.addEventListener("click", () => {
        if (turn0) {
            box.innerText = "O";
            turn0 = false;
        } else {
            box.innerText = "X";
            turn0 = true;
        }
        box.disabled = true;
        moveHistory.push({ index: index, value: box.innerText });
        redoHistory = [];
        updateUndoRedoButtons();
        checkWinner();
        checkDraw() ;
    });
});

const disableBoxes = () => {
    for (let box of boxes) {
        box.disabled = true;
    }
};

const enableBoxes = () => {
    for (let box of boxes) {
        box.disabled = false;
        box.innerText = "";
    }
};

const showWinner = (winner) => {
    msg.innerText = `Congratulations, winner is ${winner}`;
    msgContainer.classList.remove("hide");
    disableBoxes();
};

const checkDraw = () => {
    if ([...boxes].every(box => box.innerText !== "") && msgContainer.classList.contains("hide")) {
        msg.innerText = "It's a tie!";
        msgContainer.classList.remove("hide");
        disableBoxes();
    }
};


const checkWinner = () => {
    for (let pattern of winpattern) {
        let pos1Val = boxes[pattern[0]].innerText;
        let pos2Val = boxes[pattern[1]].innerText;
        let pos3Val = boxes[pattern[2]].innerText;

        if (pos1Val !== "" && pos2Val !== "" && pos3Val !== "") {
            if (pos1Val === pos2Val && pos2Val === pos3Val) {
                showWinner(pos1Val);
            }
        }
    }
};

const newGame = () => {
    msgContainer.classList.add("hide");
    resetGame();
};

const undoMove = () => {
    if (moveHistory.length === 0) return;
    let lastMove = moveHistory.pop();
    redoHistory.push(lastMove);
    let box = boxes[lastMove.index];
    box.innerText = "";
    box.disabled = false;
    turn0 = !turn0;
    updateUndoRedoButtons();
};

const redoMove = () => {
    if (redoHistory.length === 0) return;
    let lastRedo = redoHistory.pop();
    moveHistory.push(lastRedo);
    let box = boxes[lastRedo.index];
    box.innerText = lastRedo.value;
    box.disabled = true;
    turn0 = !turn0;
    updateUndoRedoButtons();
    checkWinner();
};

newgamebtn.addEventListener("click", newGame);
resetBtn.addEventListener("click", resetGame);
undoBtn.addEventListener("click", undoMove);
redoBtn.addEventListener("click", redoMove);
