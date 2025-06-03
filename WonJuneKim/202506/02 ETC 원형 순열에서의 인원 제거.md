```javascript
const fs = require("fs");
const input = fs.readFileSync(0).toString().trim().split('\n');
const [n, k] = input[0].split(" ").map(Number);

const MAX_SIZE = 10000;

class Queue {
    constructor() {
        this.q = Array(MAX_SIZE).fill(0);
        this.head = 0;
        this.tail = 0;
    }
    
    push(item) {
        if(this.full()) throw new Error("Queue is full");

        this.tail = (this.tail + 1) % MAX_SIZE;
        this.q[this.tail] = item;
    }

    full() {
        return (this.tail + 1) % MAX_SIZE === this.head;
    }

    empty() {
        return this.head === this.tail;
    }

    size() {
        return (this.tail - this.head + MAX_SIZE) % MAX_SIZE;
    }

    pop() {
        if(this.empty()) throw new Error("Queue is empty");

        this.head = (this.head + 1) % MAX_SIZE;
        return this.q[this.head];
    }

    front() {
        if (this.empty()) throw new Error("Queue is empty");

        return this.q[(this.head +1) % MAX_SIZE];
    }
}

const q = new Queue();

//큐에 남은 사람들을 넣는거
for (let i =1; i <=n; i++) {
    q.push(i);
}

let answer = "";
while (q.size() >1) {
    for (let i = 0; i<k-1; i++) {
        q.push(q.front());
        q.pop();
    }

    answer += `${q.front()} `;
    q.pop();
}

answer += `${q.front()} `;
console.log(answer);
```