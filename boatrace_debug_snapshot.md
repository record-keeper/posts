# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-04T13:00:02.460084+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×99 (24h)
- 🔴 PSI_DRIFT_DETECTED×26 (24h)
- 🔴 CALIBRATION_DRIFT×25 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-04T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×10  [2026-05-04T12:49:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×54  [2026-05-04T12:03:05]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×23  [2026-05-04T12:03:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×54  [2026-05-04T12:03:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×54  [2026-05-04T12:03:05]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×19  [2026-05-04T10:44:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×44  [2026-05-04T10:00:10]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-04T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2227 actual=0.2857 gap=-0.0630`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-04T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=7 pred=0.3232 actual=0.0000 gap=+0.3232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-04T06:00:08]
- key: `ROI_STAT|S00: n=101 hit%=21.8% hit_CI[Bonf]=[12.3,35.5]% ROI=0.82 ROI_boot95=[0.49,1.22]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-04T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=101<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-04T06:00:08]
- key: `ORPHAN_SCAN|90 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-04T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=101 pred=0.4304 actual=0.2178 error=+0.2125 (+49%) brier=0.2301 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-04T06:00:08]
- key: `CALIBRATION_LIVE|S00(win): n=101 pred=0.4304 hit=0.2178 cal_err=+0.2125 brier=0.2301 BSS=-0.35 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-04T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=41 pred=0.4462 actual=0.2195 gap=+0.2267`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-04T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.50+: n=38 pred=0.5335 actual=0.2368 gap=+0.2967`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-04T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-04T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-04T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.77MB / last modified 2026-05-04T13:00:04.657799+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
20260504: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-04 12:59:28,316 [INFO] scraper: odds3t: 120/120 parsed
2026-05-04 12:59:29,664 [INFO] scraper: odds3f: 20/20 parsed
2026-05-04 12:59:30,782 [INFO] scraper: odds2t: 30/30 parsed
2026-05-04 12:59:30,783 [INFO] scraper: odds2f: 15/15 parsed
2026-05-04 12:59:31,975 [INFO] scraper: odds_win: 6/6 parsed
2026-05-04 12:59:31,975 [INFO] scraper: fetch_race 22/2: boats=6 odds=191/191
2026-05-04 12:59:31,986 [INFO] predictor: CALIBRATION_MODE=on
2026-05-04 12:59:31,986 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-04 12:59:31,994 [INFO] run_cycle: fetched 22/2 [final]: 156 combos
2026-05-04 12:59:35,905 [INFO] scraper: odds3t: 120/120 parsed
2026-05-04 12:59:36,983 [INFO] scraper: odds3f: 20/20 parsed
2026-05-04 12:59:38,194 [INFO] scraper: odds2t: 30/30 parsed
2026-05-04 12:59:38,195 [INFO] scraper: odds2f: 15/15 parsed
2026-05-04 12:59:39,294 [INFO] scraper: odds_win: 4/6 parsed
2026-05-04 12:59:39,294 [INFO] scraper: fetch_race 10/10: boats=6 odds=189/191
2026-05-04 12:59:39,303 [INFO] predictor: CALIBRATION_MODE=on
2026-05-04 12:59:39,303 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-04 12:59:39,311 [INFO] run_cycle: fetched 10/10 [scan]: 154 combos
2026-05-04 12:59:42,881 [INFO] scraper: odds3t: 120/120 parsed
2026-05-04 12:59:44,077 [INFO] scraper: odds3f: 20/20 parsed
2026-05-04 12:59:45,181 [INFO] scraper: odds2t: 30/30 parsed
2026-05-04 12:59:45,182 [INFO] scraper: odds2f: 15/15 parsed
2026-05-04 12:59:46,287 [INFO] scraper: odds_win: 6/6 parsed
2026-05-04 12:59:46,287 [INFO] scraper: fetch_race 14/10: boats=6 odds=191/191
2026-05-04 12:59:46,298 [INFO] predictor: CALIBRATION_MODE=on
2026-05-04 12:59:46,298 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-04 12:59:46,306 [INFO] run_cycle: fetched 14/10 [scan]: 156 combos
2026-05-04 12:59:46,412 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 39
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 39
  }
]
```

## Phase別通知記録 (24h)
{'final': 12, 'result': 7, 'scan': 20}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 99
  ANOMALY_SCRAPER_FAILURE_BURST: 81
  PSI_DRIFT_DETECTED: 26
  CALIBRATION_DRIFT: 25
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  ANOMALY_SCAN_FINAL_RATIO: 11
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 9 | 14,100 | 11,580 | -2,520 | 0.821 |

## 直近アラート (24h・新しい順)
```
[12:59:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1357}
[12:58:01] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 59, "n_recent": 47, "psi": 0.986}
[12:58:01] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1361}
[12:56:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1351}
[12:55:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1334}
[12:54:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1341}
[12:53:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1324}
[12:52:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1353}
[12:51:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1331}
[12:50:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1322}
```

## 本日残レース: 144件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 216件 登録 / 72件 締切済
- 通知発射: scan=9 nid / final=6 nid / result=4 nid
- predictions: 5 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 2310R | win | 1 | 0.5334 | 4.2 | 2.24 | 300 | scan=- drift=- | 12:57:46 |
| S00 | 024R | win | 1 | 0.3177 | 8.7 | 2.76 | 300 | scan=8.5 drift=+2.4% | 12:11:32 |
| S00 | 108R | win | 1 | 0.3177 | 6.5 | 2.07 | 300 | scan=6.6 drift=-1.5% | 11:56:32 |
| S00 | 021R | win | 1 | 0.4111 | 8.0 | 3.29 | 300 | scan=13.0 drift=-38.5% | 10:44:21 |
| S00 | 103R | win | 1 | 0.5174 | 8.9 | 4.60 | 300 | scan=9.0 drift=-1.1% | 09:29:22 |
| S00 | 193R | win | 1 | 0.5174 | 5.5 | 2.85 | 300 | scan=11.2 drift=-50.9% | 16:15:21 |
| S00 | 192R | win | 1 | 0.5476 | 13.5 | 7.39 | 300 | scan=- drift=- | 15:45:22 |
| S00 | 098R | win | 1 | 0.4111 | 38.2 | 15.70 | 300 | scan=- drift=- | 13:51:44 |
| S00 | 093R | win | 1 | 0.4111 | 7.5 | 3.08 | 300 | scan=- drift=- | 11:23:22 |
| S00 | 106R | win | 1 | 0.4111 | 5.3 | 2.18 | 300 | scan=10.2 drift=-48.0% | 10:53:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 33 | -3.0% | -81.4% | +117.3% | 12 | 9 | 23 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 489.1s |
| **Latency** (scan→final max) | 609.9s |
| **Traffic** (notifications 24h) | 39 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 105 | 0.4289 | 0.2190 | +0.2098 | 🟡+49% | 0.2309 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 105 | 0.4289 | 0.2190 | 0.2309 | 🔴-0.35 | 0.842 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.20-0.30 | 7 | 0.2227 | 0.2857 | 🔴-0.0630 |
| 0.30-0.50 | 51 | 0.4236 | 0.1961 | 🔴+0.2275 |
| 0.50+ | 39 | 0.5331 | 0.2308 | 🔴+0.3023 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 5 | 0.35 |
| win | <10.0 | ✅learned | 16 | 0.61 |
| win | <20.0 | ⚠️fallback | 2 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-05-04T13:00:02.460084+09:00_