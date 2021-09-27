CREATE OR REPLACE VIEW period_view AS

	SELECT operators.endpoint_id, periods.mode_start, mode_start + interval '1' MINUTE * mode_duration as mode_end, periods.mode_duration, periods.label,  reasons.reason, operators.operator_name, energy.kwh
	FROM operators 
	LEFT JOIN reasons 
	ON reasons.event_time BETWEEN operators.login_time AND operators.logout_time
	LEFT JOIN periods
	ON periods.mode_start = reasons.event_time
	LEFT JOIN energy
	ON energy.event_time = reasons.event_time

