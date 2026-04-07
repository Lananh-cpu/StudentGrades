# StudentGrades
StudentGrades.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract StudentGrades {
    struct Student {
        string name;
        uint8 math;
        uint8 english;
        uint8 science;
        bool exists;
    }

    mapping(address => Student) public students;

    function addStudent(string memory _name, uint8 _math, uint8 _english, uint8 _science) public {
        require(!students[msg.sender].exists, "Student already exists");
        students[msg.sender] = Student(_name, _math, _english, _science, true);
    }

    function getAverage(address _student) public view returns (uint8) {
        Student memory s = students[_student];
        require(s.exists, "Student not found");
        return (s.math + s.english + s.science) / 3;
    }
}
