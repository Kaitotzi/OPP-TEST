class Student:
    def __init__(self, name, surname, gender):
        self.name = name
        self.surname = surname
        self.gender = gender
        self.finished_courses = []
        self.courses_in_progress = []
        self.grades = {}

    def __str__(self):
        return f"Student: {self.name} {self.surname}"


class Mentor:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.courses_attached = []

    def rate_hw(self, student, course, grade):
        if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
            if course in student.grades:
                student.grades[course] += [grade]
            else:
                student.grades[course] = [grade]
        else:
            return 'Ошибка'

    def __str__(self):
        return f"Mentor: {self.name} {self.surname}"


class Lecturer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.lectures_given = []

    def add_lecture(self, lecture):
        self.lectures_given.append(lecture)

    def __str__(self):
        return f"Lecturer: {self.name} {self.surname}"


class Reviewer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.reviews_given = []

    def add_review(self, review):
        self.reviews_given.append(review)

    def __str__(self):
        return f"Reviewer: {self.name} {self.surname}"


# Пример использования
best_student = Student('Ruoy', 'Eman', 'your_gender')
best_student.courses_in_progress += ['Python']

cool_mentor = Mentor('Some', 'Buddy')
cool_mentor.courses_attached += ['Python']

cool_lecturer = Lecturer('Judy', 'Hern')
cool_lecturer.courses_attached += ['Python']
cool_lecturer.add_lecture("Introduction to Python")

cool_reviewer = Reviewer('Maik', 'Wazowski')
cool_reviewer.courses_attached += ['Python']
cool_reviewer.add_review("Great job on the homework!")

cool_mentor.rate_hw(best_student, 'Python', 10)
cool_mentor.rate_hw(best_student, 'Python', 10)
cool_mentor.rate_hw(best_student, 'Python', 10)

print(best_student.grades)
print(cool_lecturer)
print(cool_reviewer)