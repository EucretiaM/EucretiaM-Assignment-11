public interface ITakeAnAssessment
{
    int Id { get; set; }
    string Name { get; set; }
    decimal AssessmentNumber { get; set; }
    string SubmitAssignment();
}
public class Assessment : ITakeAnAssessment
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }

    public string SubmitAssignment()
    {
        return $"Assessment ID: {Id}, Name: {Name}, AssessmentNumber: {AssessmentNumber}";
    }
}
public class EditAssessment
{
    private List<ITakeAnAssessment> _questions;

    public EditAssessment()
    {
        _questions = new List<ITakeAnAssessment>();
    }

    public void DeleteAnswer(ITakeAnAssessment question)
    {
        _questions.delete(question);
    }

    public void ReviewAssessment()
    {
        foreach (var question in _questions)
        {
            Console.WriteLine(question.ReviewAssessment());
        }
    }
}